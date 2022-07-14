
# Summary

The Uniswap Labs team believes the future of Web3 is multi-chain, that’s why in early 2022 we released the [scripts and instructions](https://uniswap.org/blog/multichain-uniswap) for the community to deploy the V3 Protocol to chains that have received a license exemption via governance vote. 

To continue removing Uniswap Labs as a dependency from this process and turn more power over to the community, we are releasing the complete set of instructions for deploying the V3 Protocol to a governance approved chain, and integrating seamlessly into the ecosystem.

# Where we're going
After following the instructions presented in the below sections, networks who have received approval from Uniswap Governance will have the Uniswap V3 protocol running fully on their EVM chain meaning the following is true: 

- All contracts in the [@uniswap/v3-core](https://github.com/Uniswap/v3-core) and [@uniswap/v3-periphery](https://github.com/Uniswap/v3-periphery) repos are deployed to the new chain
- The [app.uniswap.org](https://app.uniswap.org) and [info.uniswap.org](info.uniswap.org) sites include all supported functionality on the newly deployed EVM chain
- Uniswap Governance on the Ethereum Mainnet chain has an established message bridge with the deployment on the new EVM chain


[ TODO -> Create a visual / diagram of all the repos and components ] 

Teams should follow these steps sequentially for best results. 

# Deploy the V3 Protocol Contracts

The first step in setting up Uniswap V3 on a new EVM chain is to deploy the smart contracts that make up the protocol. For covnenience, the Uniswap Labs team has created a set of deployment scripts and management CLI for running it that will coordinate and deploy the necessary contracts to a new EVM chain. 

All you need to do is create the account to deploy with, fund it for gas fees (40-50M gas required), then run one command in the CLI. The script will sequentially deploy each contract, creating checkpoints as it goes that can be reverted back to in case any issues arise. 

To start a deployment follow the detailed CLI instructions here → https://github.com/Uniswap/deploy-v3

# Set Up Subgraph
[The Graph](https://thegraph.com/en/) is one of the most popular blockchain data indexing tools. If the chain you deployed to supports it, it is highly recommended that you set up a [Sub Graph](https://thegraph.com/docs/en/developer/define-subgraph-hosted/) to index Uniswap activity on the new chain. 

Having a Subgraph for your deployment not only allows integrators to access fast, reliable data, but will also make integrating with existing parts of the Uniswap Ecosystem, like [info.uniswap.org](info.uniswap.org) a seamless experience. 

Setting up a "Sub Graph" to index the Uniswap Protocol on a newly deployed chain allows users to easily query data about Uniswap activity on the new deployment and even build integrations with fast reliable data access. 

The best way to set up your Subgraph is to start with an existing one from another chain and edit it to correspond to yours. You'll then submit that to The Graph and it will start indexing. 

When you're ready to start setting up your Subgraph, follow these detailed instructions → [Setting up a Subgraph](https://github.com/Uniswap/v3-new-chain-deployments/blob/main/subgraph_instructions.md).

# Update the Auto Router

 Uniswap Labs has produced an [Auto Router API](https://github.com/Uniswap/routing-api), an off chain system that can calculate the most efficient trade routes for assets on your chain. You will need to make updates to the Routing API repo to support your chain. 

### How to Update the Auto Rotuer

Instructions for updating can be found in the Readme of the repo. 

- [ TODO ] Add instructions to https://github.com/Uniswap/routing-api

[ FAQs / Troubleshooting ]

# Create Your Token List
[Token Lists](https://tokenlists.org/) are another key primitive in the Uniswap and larger DeFi eco-system. Token Lists are a simple schema for identifying supported tokens on a dApp. 

```
{
  "name": "Example Token List",
  "timestamp": "2022-03-01T22:44:18.339Z",
  "version": {
    "major": 4,
    "minor": 2,
    "patch": 0
  },
  "tokens": [
    {
      "logoURI": "https://logo.io",
      "chainId": 42161,
      "address": "0x7cb16cb78ea464aD35c8a50ABF95dff3c9e09d5d",
      "name": "0xBitcoin Token",
      "symbol": "0xBTC",
      "decimals": 8,
      "extensions": {}
    },
    ...
    ]
}
```

As a next step in the deployment of a new chain, you will author a token list to represent the tokens supported on your chain and host it (preferably on IPFS or another decentralized system). With an up to date Token List, you can easily manage the tokens supported in the Uniswap App as well as in dApps across the ecosystem. 

Follow the instructions in the [Token Lists Package](https://github.com/Uniswap/token-lists#authoring-token-lists) to author, validate and host your token list. You'll need a valid Token List to proceed with future steps. 


# Update the Front End App

The [Uniswap App](http://app.uniswap.org) is one of the most used dApps in web3 and is where over 60% of Uniswap trading occurs. To access this user base, you’ll need to update the [open source App code](https://github.com/Uniswap/interface) to include the newly deployed chain.  

Uniswap App Repo → https://github.com/Uniswap/interface


There will be slight, specific nuances with each new chain addition but we've found that these additions have the same basic steps. As such we recommend looking at a past PR for a new chain addition (For example, the [Celo addition](https://github.com/Uniswap/interface/pull/3915/)) to understand how to implement this feature. At a high level, the steps you'll complete are: 

- **[ TODO ]**
 
 Once the necessary changes are made and you've tested the integration locally, submit a PR to the repo for review.

# Update Info Site
The [info.uniswap.org](https://info.uniswap.org)

# Create a Governance Bridge
[ Overview ] 

[ Link to Instructions ] 

[ FAQ ]

# Validate Your Deployment
[ Overview ]

# Recommended Optional Steps
[ Overview ]

# Helpful Links

- [Gov Proposal on this](https://gov.uniswap.org/t/proposed-template-for-future-cross-chain-deployment-proposals/16611)
- [Active Proposals](https://app.uniswap.org/#/vote?chain=mainnet)
- [https://gov.uniswap.org/t/proposed-template-for-future-cross-chain-deployment-proposals/16611](https://gov.uniswap.org/t/proposed-template-for-future-cross-chain-deployment-proposals/16611)

# TODO
