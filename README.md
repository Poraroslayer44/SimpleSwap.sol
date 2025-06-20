# 💱 SimpleSwap – Final Project (Module 3)

## 🧠 Description

**SimpleSwap** is a smart contract that replicates a simplified version of Uniswap.  
It allows users to:

- Add and remove liquidity between two ERC20 tokens
- Swap tokens with real-time pricing
- View price ratios and calculate output amounts

---

## 📦 Smart Contracts (Sepolia Testnet)

- **🧠 SimpleSwap Contract:**  
  [`0x445b9d8c04676E83e1eeb83ca8092327efd4a599`](https://sepolia.etherscan.io/address/0x445b9d8c04676E83e1eeb83ca8092327efd4a599#code)

- **🪙 Token A (TestTokenA):**  
  [`0x1d8Ec885fbC6446F28536ba6c3234C841Cd1f415`](https://sepolia.etherscan.io/address/0x1d8Ec885fbC6446F28536ba6c3234C841Cd1f415)

- **🪙 Token B (TestTokenB):**  
  [`0xF53FD5d7d0425Cd4d940F12774B6A3e32C0c3589`](https://sepolia.etherscan.io/address/0xF53FD5d7d0425Cd4d940F12774B6A3e32C0c3589)

---

## ⚙️ Functions Implemented

### 🔹 `addLiquidity(...)`
Adds tokenA and tokenB liquidity into the pool.
Returns actual amounts and liquidity issued.

### 🔹 `removeLiquidity(...)`
Removes liquidity from the pool and sends back the token amounts.

### 🔹 `swapExactTokensForTokens(...)`
Swaps exact amount of tokenA for tokenB using internal reserves.

### 🔹 `getPrice(...)`
Returns the price of tokenA in terms of tokenB.

### 🔹 `getAmountOut(...)`
Calculates how many tokenB units you receive when sending tokenA.

---

## 📋 Example Parameters (used in Sepolia)

### ✅ Add Liquidity
```text
amountADesired: 100000000000000000000  // 100 tokenA
amountBDesired: 100000000000000000000  // 100 tokenB
amountAMin:     95000000000000000000   // min 95 A
amountBMin:     95000000000000000000   // min 95 B
to:             0x573F181A3C105557f0A028712BEE62dC21f4Ec91
deadline:       9999999999


amountIn:       1000000000000000000     // 1 tokenA
amountOutMin:   1
path:           [tokenA, tokenB]
to:             0x573F181A3C105557f0A028712BEE62dC21f4Ec91
deadline:       9999999999


Test Steps (on Remix + MetaMask)
Deploy 2 ERC20 tokens: Token A & Token B from different contracts

Deploy SimpleSwap and save the contract address

Approve SimpleSwap to move token A and B on your behalf

Add liquidity using correct token addresses

Use swap function with exact input amount

Check balances on MetaMask or Etherscan


SimpleSwapFinal/
├── SimpleSwap.sol     # Main contract with all logic
└── README.md          # Documentation (this file)


Final Project for Blockchain Development - Module 3
Submitted by: Adriel Correa
Wallet: 0x573F181A3C105557f0A028712BEE62dC21f4Ec91
