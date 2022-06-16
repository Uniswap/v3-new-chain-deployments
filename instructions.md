
# How to Deploy Uniswap V3

The Uniswap Labs team believes the future of Web3 is multi-chain, that’s why in early 2022 we released the [scripts and instructions](https://uniswap.org/blog/multichain-uniswap) for the community to deploy the V3 Protocol to chains that have received a license exemption via governance vote. 

To continue removing Uniswap Labs as a dependency from this process and turn more power over to the community, we are releasing the complete set of instructions for deploying the V3 Protocol to a governance approved chain, and integrating seamlessly into the ecosystem.

# The Process

The following sections outline the process for deploying the Uniswap V3 Protocol and integrating into the existing ecosystem including making it available for trading on [app.uniswap.org](http://app.uniswap.org), [info.uniswap.org](http://info.uniswap.org) and creating a Subgraph for it’s data. 

[ TODO -> Create a visual / diagram of all the repos and components ] 

Teams should follow these steps sequentially for best results. 

## 1. Deploy the V3 Protocol Contracts

The first step in setting up Uniswap V3 on a new chain is to deploy the smart contracts that make up the protocol. The Uniswap Labs team has created a script that handles this process for you. 

All you need to do is create the account to deploy with, fund it for gas fees, then use it to run the script below. 

### Script & Instructions

- Instructions for Deploying → https://github.com/Uniswap/deploy-v3

### FAQs

- ***How much gas should I expect to use for full completion?***
We estimate 30M - 40M gas needed to run the full deploy script.
- ***When I run the script, it says "Contract was already deployed..."***
Delete state.json before a fresh deploy. state.json tracks which steps have already occurred. If there are any entries, the deploy script will attempt to pick up from the last step in state.json.
- ***Where can I see all the addresses where each contract is deployed?***
Check out state.json. It'll show you the final deployed addresses.
- ***How long will the script take?***
Depends on the confirmation times and gas parameter. The deploy script sends up to a total of 14 transactions.
- ***Where should I ask questions or report issues?***
You can file them in issues on this repo and we'll try our best to respond.

## 2. Set Up Subgraph

Although not required for running the protocol, off chain data plays an important role in building the ecosystem around Uniswap V3 on new chains. Many tools in the ecosystem rely on [The Graph](https://thegraph.com/en/) data for analytics and even running apps. 

For this reason we highly recommend setting up a Sub Graph for your new deployment if your chain is supported.

### Setting up your Sub Graph

- Instructions for setting up a subgraph →

[Creating Subgraph For New Uniswap Deployment](https://github.com/Uniswap/v3-new-chain-deployments/blob/main/subgraph_instructions.md)

## 3. Update the Auto Router

 Uniswap Labs has produced an [Auto Router API](https://github.com/Uniswap/routing-api), an off chain system that can calculate the most efficient trade routes for assets on your chain. You will need to make updates to the Routing API repo to support your chain. 

### How to Update the Auto Rotuer

Instructions for updating can be found in the Readme of the repo. 

- [ TODO ] Add instructions to https://github.com/Uniswap/routing-api

[ FAQs / Troubleshooting ]

## 4. Create Your Token List
[ Overview ] 

[ Link to Instructions ] 

[ FAQ ]

## 5. Update the Front End App

The [Uniswap App](http://app.uniswap.org) is one of the most used dApps in web3 and is where over 60% of Uniswap trading occurs. To access this user base, you’ll need to update the open source App code to 
 

Link to Instructions → [ TODO ] Add section to https://github.com/Uniswap/interface 

[ FAQs / Troubleshooting ]

## 6. Create a Governance Bridge
[ Overview ] 

[ Link to Instructions ] 

[ FAQ ]

# Helpful Links

- [Gov Proposal on this](https://gov.uniswap.org/t/proposed-template-for-future-cross-chain-deployment-proposals/16611)
- [Active Proposals](https://app.uniswap.org/#/vote?chain=mainnet)
- [https://gov.uniswap.org/t/proposed-template-for-future-cross-chain-deployment-proposals/16611](https://gov.uniswap.org/t/proposed-template-for-future-cross-chain-deployment-proposals/16611)

# TODO
- Set links back to master versions when pushing
