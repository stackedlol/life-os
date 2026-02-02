---
tags: economics
---

the code layer that powers DeFi - extends [[bitcoin]] and [[decentralization]]

### what are smart contracts?
- programs that run on a blockchain
- self-executing code with rules that can't be changed
- "if this, then that" but enforced by math, not trust
- the foundation of DeFi, NFTs, DAOs, and on-chain apps

### why they matter for profit
- DeFi is just smart contracts moving money
- reading contracts = understanding real mechanics (not marketing)
- finding bugs = finding opportunities (or avoiding losses)
- automation without intermediaries = new profit models

### ethereum virtual machine (EVM)
- the computer that runs smart contracts
- ethereum, polygon, arbitrum, BSC all use EVM
- contracts compile to bytecode, run on every node
- deterministic: same input always gives same output

### gas: the cost of computation
- every operation costs gas
- gas price fluctuates with demand
```
transaction cost = gas used × gas price
```
- complex contracts = more gas = higher cost
- gas optimization is critical for profitability
- failed transactions still cost gas

### solidity basics
- most common smart contract language
- looks like JavaScript with types
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    uint256 public storedValue;

    function set(uint256 _value) public {
        storedValue = _value;
    }

    function get() public view returns (uint256) {
        return storedValue;
    }
}
```

### key solidity concepts

#### data types
```solidity
uint256 number;        // unsigned integer (most common)
int256 negative;       // signed integer
address wallet;        // ethereum address (20 bytes)
bool flag;             // true/false
string text;           // dynamic string
bytes32 hash;          // fixed-size byte array
mapping(address => uint256) balances;  // key-value store
```

#### visibility
- `public` - anyone can call
- `private` - only this contract
- `internal` - this contract + children
- `external` - only external calls (cheaper gas)

#### functions
```solidity
// view: reads state, no gas if called externally
function getBalance() public view returns (uint256) {
    return balances[msg.sender];
}

// pure: no state access, just computation
function add(uint256 a, uint256 b) public pure returns (uint256) {
    return a + b;
}

// payable: can receive ETH
function deposit() public payable {
    balances[msg.sender] += msg.value;
}
```

#### important globals
```solidity
msg.sender   // address that called the function
msg.value    // ETH sent with the call
block.timestamp  // current block time
block.number // current block number
tx.origin    // original sender (avoid using - security risk)
```

### ERC standards

#### ERC-20: fungible tokens
- the standard for tokens (USDC, LINK, UNI)
- key functions:
```solidity
function transfer(address to, uint256 amount) external returns (bool);
function approve(address spender, uint256 amount) external returns (bool);
function transferFrom(address from, address to, uint256 amount) external returns (bool);
function balanceOf(address account) external view returns (uint256);
```
- approve + transferFrom = allowing contracts to spend your tokens

#### ERC-721: NFTs
- non-fungible tokens, each unique
- ownerOf, transferFrom, approve
- tokenURI points to metadata

#### ERC-1155: multi-token
- batch transfers, both fungible and non-fungible
- more gas efficient for games/collections

### DeFi primitives

#### AMM (automated market maker)
- from [[market-microstructure]]: DEXs use AMMs instead of order books
```solidity
// simplified constant product AMM
function swap(uint256 amountIn) external returns (uint256 amountOut) {
    uint256 reserveIn = tokenA.balanceOf(address(this));
    uint256 reserveOut = tokenB.balanceOf(address(this));

    // x * y = k formula
    amountOut = (amountIn * reserveOut) / (reserveIn + amountIn);

    tokenA.transferFrom(msg.sender, address(this), amountIn);
    tokenB.transfer(msg.sender, amountOut);
}
```

#### lending protocols
- deposit collateral, borrow assets
- liquidation if collateral value drops
- interest rates set by supply/demand curves
- examples: Aave, Compound

#### yield farming
- provide liquidity, earn rewards
- often token incentives on top of fees
- impermanent loss is the hidden cost

### reading contracts

#### where to find them
- **Etherscan** - verified source code for mainnet
- **GitHub** - protocol repositories
- **Block explorers** - Polygonscan, Arbiscan, etc.

#### what to look for
1. **owner/admin functions** - who has control?
2. **upgradeability** - can the code change?
3. **token approvals** - what can spend your tokens?
4. **withdrawal functions** - can you get your money out?
5. **hardcoded addresses** - dependencies on other contracts

#### red flags
- unverified source code
- owner can drain funds
- unlimited token approvals
- no timelock on admin functions
- copy-pasted code with modifications

### common vulnerabilities

#### reentrancy
- attacker re-enters function before state updates
- the DAO hack was reentrancy
```solidity
// vulnerable
function withdraw() external {
    uint256 balance = balances[msg.sender];
    (bool success, ) = msg.sender.call{value: balance}("");
    balances[msg.sender] = 0;  // too late!
}

// safe: update state first
function withdraw() external {
    uint256 balance = balances[msg.sender];
    balances[msg.sender] = 0;  // update first
    (bool success, ) = msg.sender.call{value: balance}("");
}
```

#### flash loan attacks
- borrow millions, manipulate price, profit, repay
- all in one transaction
- exploits price oracle weaknesses

#### oracle manipulation
- protocols need external price data
- manipulating the oracle = manipulating the protocol
- use decentralized oracles (Chainlink) not spot prices

#### approval exploits
- unlimited approvals let contracts drain your wallet
- always check what you're approving
- revoke old approvals (revoke.cash)

#### front-running
- from [[market-microstructure]]: seeing pending transactions
- copy profitable trades, submit with higher gas
- sandwich attacks: front-run + back-run

### MEV (maximal extractable value)
- profit from ordering/including/excluding transactions
- miners/validators extract MEV
- sources: arbitrage, liquidations, sandwich attacks
```
you submit: buy 10 ETH at market
attacker sees pending tx
attacker: buy ETH (price rises)
your tx: buy ETH (worse price)
attacker: sell ETH (profit)
```
- protection: use private mempools, MEV-aware DEXs

### tools for contract analysis

#### reading/verification
- **Etherscan** - read verified source, check transactions
- **Tenderly** - simulate transactions, debug
- **DeFiLlama** - protocol TVL, analytics

#### development
- **Remix** - browser-based IDE
- **Hardhat** - development framework
- **Foundry** - fast testing framework

#### security
- **Slither** - static analysis
- **Mythril** - security scanner
- **Audit reports** - read before depositing

### practical workflow for evaluating protocols

1. **find the contracts** - Etherscan, docs, GitHub
2. **check verification** - is source code visible?
3. **read admin functions** - who controls what?
4. **check upgradeability** - can code change?
5. **read audit reports** - what did auditors find?
6. **check TVL history** - on DeFiLlama
7. **search for exploits** - rekt.news, Twitter

### building on-chain tools
- your coding skills + contract knowledge = edge
- ideas:
  - monitor whale wallets for copy trading
  - track liquidation levels
  - arbitrage scanners across DEXs
  - protocol health dashboards
- interact via: ethers.js, web3.py, viem

### connection to other notes
- [[market-microstructure]] - AMMs are microstructure
- [[automated-trading]] - bots can execute on-chain
- [[expected-value]] - protocol risks need EV analysis
- [[prediction-markets]] - Polymarket settles on-chain

### key takeaways
1. smart contracts are just code - you can read them
2. reading contracts > reading marketing
3. understand ERC-20 approvals (they're dangerous)
4. MEV exists - use protection or lose money
5. verify source code before depositing
6. admin keys and upgradeability = trust assumptions
7. your coding skills transfer directly to on-chain edges
