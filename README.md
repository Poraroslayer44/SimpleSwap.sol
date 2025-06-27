# SimpleSwap - Trabajo Final Módulo 3

Este repositorio contiene el contrato inteligente **SimpleSwap**, desarrollado como Trabajo Final del Módulo 3 del curso de Blockchain. El contrato permite agregar y remover liquidez, intercambiar tokens, obtener precios y calcular cantidades de salida, replicando la funcionalidad básica de Uniswap sin depender de su protocolo.

## Objetivo

Crear un DEX básico (intercambiador descentralizado) entre dos tokens ERC-20, permitiendo a los usuarios:

- Agregar liquidez.
- Remover liquidez.
- Intercambiar tokens.
- Obtener precios.
- Calcular cantidades de salida.

---

## 🔗 Contratos desplegados

- Contrato `SimpleSwap`: [ENLACE_A_SEPOLIA_ETHERSCAN][https://sepolia.etherscan.io/address/0x445b9d8c04676E83e1eeb83ca8092327efd4a599#code](https://sepolia.etherscan.io/address/0x445b9d8c04676E83e1eeb83ca8092327efd4a599))
- Token A (`TestTokenA`): [ENLACE_TOKEN_A]([https://sepolia.etherscan.io/address/...](https://sepolia.etherscan.io/address/0x1d8Ec885fbC6446F28536ba6c3234C841Cd1f415)
- Token B (`TestTokenB`): [ENLACE_TOKEN_B]([https://sepolia.etherscan.io/address/...](https://sepolia.etherscan.io/address/0x1d8Ec885fbC6446F28536ba6c3234C841Cd1f415)

---

## ⚙️ Funcionalidades principales

### 1️⃣ Agregar Liquidez

```solidity
function addLiquidity(
    uint amountADesired,
    uint amountBDesired,
    uint amountAMin,
    uint amountBMin,
    address to,
    uint deadline
) external returns (uint amountA, uint amountB, uint liquidity);

function removeLiquidity(
    uint liquidity,
    uint amountAMin,
    uint amountBMin,
    address to,
    uint deadline
) external returns (uint amountA, uint amountB);

function swapExactTokensForTokens(
    uint amountIn,
    uint amountOutMin,
    address[] calldata path,
    address to,
    uint deadline
) external returns (uint amountOut);

function getPrice(address tokenA, address tokenB) external view returns (uint price);

function getAmountOut(uint amountIn, uint reserveIn, uint reserveOut) public pure returns (uint amountOut);

🛠 Cómo desplegar
Deploy los tokens TestTokenA.sol y TestTokenB.sol (usando Remix).

Deploy el contrato SimpleSwap.sol, pasándole en el constructor las direcciones de los tokens.

Agregar liquidez llamando a addLiquidity desde una cuenta con tokens A y B.

Interactuar con las otras funciones para testear intercambios y precios.

Archivos
SimpleSwap.sol: contrato principal de intercambio.

TestTokenA.sol: token ERC-20 que se entrega al deployer.

TestTokenB.sol: token ERC-20 que se entrega a una address inicial.

README.md: este archivo.

Verificación
El contrato ha sido verificado correctamente en Etherscan con los siguientes parámetros:

Compiler: v0.8.20+commit.a1b79de6

Optimization: false

Runs: 200

 Comentarios
El contrato incluye comentarios explicativos en inglés.

Los nombres de funciones, variables y eventos siguen buenas prácticas.

Todos los tokens utilizados son compatibles con ERC-20.

La función getPrice() fue adaptada al formato solicitado.

Adriel Joaquín Correa Nacusi
Trabajo Final - Módulo 3

Licencia
Este proyecto está licenciado bajo la licencia MIT.


