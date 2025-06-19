// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

contract SimpleSwap {
    address public tokenA;
    address public tokenB;

    uint256 public reserveA;
    uint256 public reserveB;

    uint256 public totalLiquidity;
    mapping(address => uint256) public liquidity;

    constructor(address _tokenA, address _tokenB) {
        tokenA = _tokenA;
        tokenB = _tokenB;
    }

    function addLiquidity(
        uint256 amountADesired,
        uint256 amountBDesired,
        uint256 amountAMin,
        uint256 amountBMin,
        address to,
        uint256 deadline
    ) external returns (uint256 amountA, uint256 amountB, uint256 liquidityMinted) {
        require(block.timestamp <= deadline, "Deadline passed");
        require(amountADesired >= amountAMin, "amountADesired < amountAMin");
        require(amountBDesired >= amountBMin, "amountBDesired < amountBMin");
        require(IERC20(tokenA).balanceOf(msg.sender) >= amountADesired, "Not enough tokenA");
        require(IERC20(tokenB).balanceOf(msg.sender) >= amountBDesired, "Not enough tokenB");
        require(IERC20(tokenA).allowance(msg.sender, address(this)) >= amountADesired, "Approve tokenA first");
        require(IERC20(tokenB).allowance(msg.sender, address(this)) >= amountBDesired, "Approve tokenB first");

        IERC20(tokenA).transferFrom(msg.sender, address(this), amountADesired);
        IERC20(tokenB).transferFrom(msg.sender, address(this), amountBDesired);

        amountA = amountADesired;
        amountB = amountBDesired;

        uint256 liquidityAdded;
        if (totalLiquidity == 0) {
            liquidityAdded = sqrt(amountA * amountB);
        } else {
            liquidityAdded = min(
                (amountA * totalLiquidity) / reserveA,
                (amountB * totalLiquidity) / reserveB
            );
        }

        require(liquidityAdded > 0, "Insufficient liquidity minted");

        reserveA += amountA;
        reserveB += amountB;

        totalLiquidity += liquidityAdded;
        liquidity[to] += liquidityAdded;

        return (amountA, amountB, liquidityAdded);
    }

    function removeLiquidity(
        uint256 liquidityAmount,
        uint256 amountAMin,
        uint256 amountBMin,
        address to,
        uint256 deadline
    ) external returns (uint256 amountA, uint256 amountB) {
        require(block.timestamp <= deadline, "Deadline passed");
        require(liquidity[msg.sender] >= liquidityAmount, "Not enough liquidity");

        amountA = (liquidityAmount * reserveA) / totalLiquidity;
        amountB = (liquidityAmount * reserveB) / totalLiquidity;

        require(amountA >= amountAMin, "amountA < min");
        require(amountB >= amountBMin, "amountB < min");

        liquidity[msg.sender] -= liquidityAmount;
        totalLiquidity -= liquidityAmount;

        reserveA -= amountA;
        reserveB -= amountB;

        IERC20(tokenA).transfer(to, amountA);
        IERC20(tokenB).transfer(to, amountB);

        return (amountA, amountB);
    }

    function swapExactTokensForTokens(
        uint256 amountIn,
        uint256 amountOutMin,
        address[] calldata path,
        address to,
        uint256 deadline
    ) external returns (uint256 amountOut) {
        require(path.length == 2, "Path must be [tokenIn, tokenOut]");
        require(block.timestamp <= deadline, "Deadline passed");

        address input = path[0];
        address output = path[1];
        require((input == tokenA && output == tokenB) || (input == tokenB && output == tokenA), "Invalid path");

        bool isAToB = input == tokenA;

        uint256 reserveIn = isAToB ? reserveA : reserveB;
        uint256 reserveOut = isAToB ? reserveB : reserveA;

        IERC20(input).transferFrom(msg.sender, address(this), amountIn);

        amountOut = getAmountOut(amountIn, reserveIn, reserveOut);
        require(amountOut >= amountOutMin, "Insufficient output amount");

        IERC20(output).transfer(to, amountOut);

        if (isAToB) {
            reserveA += amountIn;
            reserveB -= amountOut;
        } else {
            reserveB += amountIn;
            reserveA -= amountOut;
        }

        return amountOut;
    }

    function getPrice() external view returns (uint256 price) {
        require(reserveA > 0 && reserveB > 0, "No liquidity");
        return (reserveB * 1e18) / reserveA;
    }

    function getAmountOut(uint256 amountIn, uint256 reserveIn, uint256 reserveOut) public pure returns (uint256) {
        require(amountIn > 0, "Insufficient input");
        require(reserveIn > 0 && reserveOut > 0, "Insufficient liquidity");
        uint256 amountInWithFee = amountIn * 997;
        uint256 numerator = amountInWithFee * reserveOut;
        uint256 denominator = (reserveIn * 1000) + amountInWithFee;
        return numerator / denominator;
    }

    function min(uint256 a, uint256 b) internal pure returns (uint256) {
        return a < b ? a : b;
    }

    function sqrt(uint256 y) internal pure returns (uint256 z) {
        if (y > 3) {
            z = y;
            uint256 x = y / 2 + 1;
            while (x < z) {
                z = x;
                x = (y / x + x) / 2;
            }
        } else if (y != 0) {
            z = 1;
        }
    }
}
