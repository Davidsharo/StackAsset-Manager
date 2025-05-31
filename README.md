

# StackAsset-Manager - DeFi Asset Management Platform

## Overview

This smart contract implements a decentralized finance (DeFi) asset management platform on the Stacks blockchain. It allows the contract administrator to mint new tokens representing various assets, manage token prices with historical tracking, and facilitate secure token transfers including allowance-based spending.

---

## Features

* **Token Minting:** Admin can create new tokens with customizable names, categories, maximum supply, and initial prices.
* **Price Management:** Admin can update token prices, with each update recorded along with a timestamp to maintain price history.
* **Token Balances:** Tracks token balances per holder and token.
* **Allowance System:** Token holders can authorize other principals to spend a specified amount of their tokens.
* **Token Transfers:** Supports direct transfers and transfers via authorized spenders.
* **Administrative Controls:** Only the contract admin can mint tokens and update prices, and can transfer admin rights.

---

## Data Structures

* **Tokens (`tokens`):** Stores token metadata including name, category, max supply, current price, and last price update timestamp.
* **Balances (`balances`):** Tracks token amounts held by principals.
* **Allowances (`allowances`):** Records spending permissions granted by token holders to authorized principals.
* **Price History (`price-history`):** Logs historical token prices with timestamps.
* **Contract Admin:** Principal who controls sensitive functions like minting and price updating.
* **Token Counter:** Auto-incrementing token ID tracker.

---

## Constants & Error Codes

| Error Code | Description                |
| ---------- | -------------------------- |
| u100       | Not authorized             |
| u101       | Token already exists       |
| u102       | Token not found            |
| u103       | Insufficient funds         |
| u104       | Invalid token name         |
| u105       | Invalid token category     |
| u106       | Invalid max supply         |
| u107       | Invalid token price        |
| u108       | Invalid recipient          |
| u109       | Invalid transfer amount    |
| u110       | Insufficient allowance     |
| u111       | Invalid authorized address |
| u112       | Invalid price update       |

---

## Public Functions

### `mint-token`

Create a new token with specified parameters. Only the admin can mint tokens.

* **Inputs:**

  * `token-name` (string-ascii 64)
  * `token-category` (string-ascii 32)
  * `max-supply` (uint)
  * `token-price` (uint)
* **Output:** Newly minted token ID or error.

### `update-token-price`

Update the price of an existing token. Only admin authorized.

* **Inputs:**

  * `token-id` (uint)
  * `new-price` (uint)
* **Output:** Success boolean or error.

### `authorize-spending`

Grant permission to another principal to spend tokens on behalf of the caller.

* **Inputs:**

  * `authorized` (principal)
  * `token-id` (uint)
  * `allowed-amount` (uint)
* **Output:** Success boolean.

### `transfer`

Transfer tokens from caller to recipient.

* **Inputs:**

  * `recipient` (principal)
  * `token-id` (uint)
  * `transfer-amount` (uint)
* **Output:** Success boolean or error.

### `transfer-as-authorized`

Transfer tokens from another principal as an authorized spender.

* **Inputs:**

  * `from` (principal)
  * `recipient` (principal)
  * `token-id` (uint)
  * `transfer-amount` (uint)
* **Output:** Success boolean or error.

### `set-contract-admin`

Change the contract administrator.

* **Inputs:**

  * `new-admin` (principal)
* **Output:** Success boolean or error.

---

## Read-Only Functions

* `get-price-at-time(token-id, timestamp)`: Get historical price of a token at a specific timestamp.
* `is-valid-token(token-id)`: Check if a token exists.
* `get-authorized-amount(holder, authorized, token-id)`: Get allowance amount.
* `get-token-details(token-id)`: Retrieve token metadata.
* `get-holder-balance(holder, token-id)`: Get the token balance of a holder.

---

## Usage Notes

* The contract admin has exclusive rights to mint tokens and update prices.
* Token holders can authorize other principals to spend tokens on their behalf, facilitating DeFi use cases like automated trading or staking.
* Historical price data enables advanced analytics and auditing.
* Token transfers prevent sending tokens to self or invalid amounts.
* Proper error handling ensures secure and predictable contract behavior.

---

## Future Enhancements (Suggestions)

* Add staking or yield farming capabilities.
* Implement token burning.
* Support batch transfers.
* Enable decentralized governance for admin roles.
* Integrate with external price oracles.

---
