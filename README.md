# SimpleSwap.sol

# 🧪 SimpleSwap – Final Project Module 3

Smart contract developed as a final project for Module 3. It replicates basic Uniswap functions such as adding/removing liquidity, swapping ERC20 tokens, price calculation, and output estimation.

## 🚀 Contract Address

**SimpleSwap:**  
`0x445b9d8c04676E83e1eeb83ca8092327efd4a599`

**ERC20 Token A:**  
`0x1d8Ec885fbC6446F28536ba6c3234C841Cd1f415`

**ERC20 Token B:**  
`0xF53FD5d7d0425Cd4d940F12774B6A3e32C0c3589`

## ⚙️ Features

- `addLiquidity(address tokenA, address tokenB, ...)`: Add token pairs to the pool.
- `removeLiquidity(address tokenA, address tokenB, ...)`: Withdraw liquidity from the pool.
- `swapExactTokensForTokens(uint amountIn, ...)`: Swap a fixed input of tokens.
- `getPrice(address tokenA, address tokenB)`: Get price of token A in terms of B.
- `getAmountOut(uint amountIn, uint reserveIn, uint reserveOut)`: Simulate swap output.

## 🧑‍💻 Deployment & Usage

### 1. Deploy Tokens
- Use Remix and MetaMask to deploy two ERC20 tokens with 18 decimals.
- Make sure each token has a different name and symbol.

### 2. Deploy SimpleSwap
- Deploy `SimpleSwap.sol` using Remix.

### 3. Add Liquidity

```js
amountADesired: 100000000000000000000
amountBDesired: 100000000000000000000
amountAMin:     95000000000000000000
amountBMin:     95000000000000000000
to:             0xYourAddress
deadline:       9999999999

approve("0x445b9d8c04676E83e1eeb83ca8092327efd4a599", amount)

amountIn:     10000000000000000000
amountOutMin: 1
path: [
  "0x1d8Ec885fbC6446F28536ba6c3234C841Cd1f415", 
  "0xF53FD5d7d0425Cd4d940F12774B6A3e32C0c3589"
]
to:       0xYourAddress
deadline: 9999999999


getPrice(tokenA, tokenB)

getAmountOut(amountIn, reserveIn, reserveOut)

getAmountOut(amountIn, reserveIn, reserveOut)

All tokens have 18 decimals.

Approve is required before swap or liquidity operations.

All functions are commented in English following NatSpec standard.


All contracts were deployed and verified using Remix + Sepolia.

Verified source code available on Etherscan

