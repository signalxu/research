---
titel: Research on RPIP-13
discussion: https://dao.rocketpool.net/t/some-thoughts-about-rpip-13/2688/1
---

# Background

After the Rocke Pool deposit pool limit was increased once, it is currently frequently at full capacity. In such instances, users are unable to mint rETH by staking ETH, they can only obtain ETH through swaps on a DEX. This has, to a certain extent, impacted the supply of rETH. If one desires to utilize the ETH in the deposit pool, one option is for users to perform unstake operations. However, this is undesirable as it not only fails to increase the rETH supply but also diminishes it. Another alternative is to boost the supply from node operators(NOs), which not only augments the rETH supply but also enhances ETH efficiency. [RPIP-13](https://rpips.rocketpool.net/RPIPs/RPIP-13) is precisely aimed at addressing how to increase the supply from node operators. Therefore, the ensuing discussion primarily focuses on strategies to amplify the supply from node operators and reduce the entry barrier for them.

# Prior Art

## Stakewise

Stakewise offers Vault functionality to assist solo validators. The Vault is primarily managed by the node operator, and users can stake ETH in the vault. The node operator can utilize the ETH staked by users in the vault to run the validator. The vault will have a rating, which will affect the user's LST minting ratio.

Node operators do not require additional bonding and staking. However, each vault and the official staking pool of Stakewise are isolated, meaning nodes cannot obtain ETH from Stakewise's official staking pool to run validators.


## Puffer

Puffer introduces the concept of validator tickets. To run a validator with 32 ETH from the pool, a node operator needs to purchase a ticket. Each ticket grants one day of permission to operate a validator, with an initial threshold set at 28 tickets. Additionally, validators require a staking of 1-2 ETH.

Validator tickets essentially pre-advance the earnings for node operators running validators, which may disadvantage solo node operators and favor professional entities.

Validator tickets support secondary trading, potentially creating arbitrage opportunities. The pricing of tickets is determined based on the historical earnings of the market over a specific period, leading to potential price differentials.

The introduction of validator tickets has the benefit of enhancing the liquidity of ETH. For instance, while RocketPool currently requires a staking of 8 ETH, which doesn't convert to LST, using validator tickets pre-advances the staking, reducing bonding and increasing liquidity.

## Nodeset

Built on top of Rocket Pool is a matching pool that can match RPL, ETH, and node operators. However, it currently relies mainly on admin for reviewing and managing node operators.

Building something similar would require a contract audit and users trusting it. Also, users don't receive rETH directly and need to establish liquidity on a DEX, introducing significant uncertainty. Can Rocket Pool create a more native model directly?

# Related Technology

## EIP-7002

Currently, triggering the withdrawal of a validator poses several challenges. Firstly, one needs the validator key, and secondly, it cannot be directly triggered from the execution layer contract. It requires an off-chain service to monitor execution layer logs and then trigger the validator's withdrawal off-chain. EIP-7002, on the other hand, allows the direct triggering of validator withdrawal from the execution layer. This way, when oDAO indexes the validator's balance, it can simultaneously index the validator's operational status. If the validator remains offline for an extended period, it can be reported to the execution layer, triggering the validator's withdrawal and thereby safeguarding assets.

## Secure-Signer TEE

Secure-Signer is a remote-signing tool that manages validator keys on behalf of the consensus client. It can run locally with the consensus client or on a remote server. From the point of view of a node operator, there is little difference in setting up their validator. If they have SGX-enabled hardware, they can install and run Secure-Signer and instruct their consensus client of choice to use Secure-Signer as the remote-signer.

## EIP-3076

A standard format for transferring a key’s signing history allows validators to easily switch between clients without the risk of signing conflicting messages. While a common keystore format provides part of the solution, it does not contain any information about a key’s signing history. For a validator moving their keys from client A to client B, this could lead to scenarios in which client B inadvertently signs a message that conflicts with an earlier message signed with client A. The interchange format described here provides a solution to this problem.

# Specification

[] todo

