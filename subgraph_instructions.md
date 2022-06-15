# Deploying Subgraph For New Uniswap Deployment

1. See The Graph documentation for overview on The Graph [here](https://thegraph.com/docs/en/developer/quick-start/)
    1. Note: The Graph only supports a subset of networks, so check that the network of interest is supported. 
2. Fork the Uniswap subgraph code [here](https://github.com/Uniswap/v3-subgraph) . 
3. You’ll need to make a series of changes to the mappings and constants in order for you subgraph to work with the new network
    1. Change all network dependent values in the subgraph.yaml file [https://github.com/Uniswap/v3-subgraph/blob/main/subgraph.yaml](https://github.com/Uniswap/v3-subgraph/blob/main/subgraph.yaml), this includes 
        1.  Remove the `graft` helper instruction
        2. change `network` to correct network in all locations
        3. update address for `factory`, `NonfungiblePositionManager`
    2. Update all pricing constants [here](https://github.com/Uniswap/v3-subgraph/blob/bf03f940f17c3d32ee58bd37386f26713cff21e2/src/utils/pricing.ts#L7)
        1. `WETH_ADDRESS` should be the wrapped native currency equivilant for new network
        2. `USDC_WETH_03_POOL` should be some reliable pool to derive the price of token in previous step 
        3. `WHITELIST_TOKENS` should be tokens that are expected to have accurate prices (well arbitraged pools), this is used to derive USD values so extra precaution needs to be used to ensure the quality of the data 
        4. `STABLE_COINS` are token addresses for any stabelcoins used in USD heuristic 
        5. `FACTORY_ADDRESS` should be updated [here](https://github.com/Uniswap/v3-subgraph/blob/bf03f940f17c3d32ee58bd37386f26713cff21e2/src/utils/constants.ts#L6)
        6. Static token definitions should be updated [here](https://github.com/Uniswap/v3-subgraph/blob/main/src/utils/staticTokenDefinition.ts), these are used to hard code tokens that may have issues contracts that effect name or symbol value returns (can leave empty if no issues are known)
4. Follow rest of Graph documentation to deploy at an endpoint of your chosing in your own graph account 
5. Notes: 
    1. If you desire this to be used in official Uniswap sites (info), open up these changes as a PR in the subgraph repo 
    2. an optimized subgraph spec is written here but is currently untested [https://github.com/Uniswap/v3-subgraph/tree/mainnet-2.0](https://github.com/Uniswap/v3-subgraph/tree/mainnet-2.0)
