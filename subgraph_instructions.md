# Deploying the Subgraphs

## Brief
The [block indexer subgraph](https://github.com/ianlapham/blocks-subgraph) is used by info.uniswap to pull information on the latest blocks e.g. number, timestamp, size, etc.
The [v3-subgraph](https://github.com/Uniswap/v3-subgraph) is used by the smart-order-router, info.unisawp, and the interface predominantly for indexing information on pools e.g. tick data & liquidity depth, latest transactions, routing, etc.

Both of these subgraphs must be configured and deployed for new chain integrations. 

Before diving in make sure too:
* Confirm the chain you are integrating is supported by the graph 
* Create an account on the graph


## Block Indexer Instructions
1. Fork the [blocks-subgraph](https://github.com/ianlapham/blocks-subgraph)
2. Deploy a simple dummy contract on the respective chain which will be used as a point of reference by the subgraph when indexing block data. It can be an existing contract although, the ABI is required to proceed. Replace the existing ABI 'ConverterRegistryContract.json' with the one from your dummy contract deployment.
3. Change the 'abi' values in subgraph.yaml to the name of the abi file you have added. 
4. Adjust the 'startBlock' key values in subgraph.yaml to the block number before your Uniswap v3CoreFactoryAddress deployment.
5. Add a script to the package.json file that includes your access token e.g.'
   >"deploy-to-new-chain": "graph deploy --access-token ${ACCESS_TOKEN} ${github-username}/${subgraph-name} --ipfs https://api.thegraph.com/ipfs/ --node https://api.thegraph.com/deploy/ --debug"
6. Finally, run in order: 'yarn install', 'yarn codegen', 'yarn build' then 'yarn deploy-to-new-chain'

## V3-subgraph Instructions
1. Fork Uniswap's [v3-subgraph](https://github.com/Uniswap/v3-subgraph) . 
2. You’ll need to make a series of changes to the mappings and constants in order for your subgraph to work with the new network:
    1. Change all network dependent values in the subgraph.yaml file [https://github.com/Uniswap/v3-subgraph/blob/main/subgraph.yaml](https://github.com/Uniswap/v3-subgraph/blob/main/subgraph.yaml), this includes 
        1.  Remove the `graft` helper instruction
        2. change `network` to correct network in all locations
        3. update address for `factory`, `NonfungiblePositionManager`
    2. Update all pricing constants [here](https://github.com/Uniswap/v3-subgraph/blob/bf03f940f17c3d32ee58bd37386f26713cff21e2/src/utils/pricing.ts#L7)
        1. `WETH_ADDRESS` should be the wrapped native currency equivalent for new network
        2. `USDC_WETH_03_POOL` should be some reliable pool to derive the price of token in previous step 
        3. `WHITELIST_TOKENS` should be tokens that are expected to have accurate prices (well arbitraged pools), this is used to derive USD values so extra precaution needs to be used to ensure the quality of the data 
        4. `STABLE_COINS` are token addresses for any stabelcoins used in USD heuristic 
        5. `FACTORY_ADDRESS` should be updated [here](https://github.com/Uniswap/v3-subgraph/blob/bf03f940f17c3d32ee58bd37386f26713cff21e2/src/utils/constants.ts#L6)
        6. Static token definitions should be updated [here](https://github.com/Uniswap/v3-subgraph/blob/main/src/utils/staticTokenDefinition.ts), these are used to hard code tokens that may have issues contracts that effect name or symbol value returns (can leave empty if no issues are known)
3. Follow the rest of Graph documentation to deploy at an endpoint of your choosing in your own graph account 
4. Notes: 
    1. If you desire this to be used in official Uniswap sites (info), open up these changes as a PR in the subgraph repo 
    2. an optimized subgraph spec is written here but is currently untested [https://github.com/Uniswap/v3-subgraph/tree/mainnet-2.0](https://github.com/Uniswap/v3-subgraph/tree/mainnet-2.0)
