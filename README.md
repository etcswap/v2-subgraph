# ETCswap V2 Subgraph

Subgraph for indexing ETCswap V2 on-chain data on Ethereum Classic. Tracks pairs, tokens, transactions, liquidity, and historical analytics.

Forked from [Uniswap V2 Subgraph](https://github.com/Uniswap/v2-subgraph) with ETC-specific pricing (WETC, USC) in the `etcswap` branch.

## Status: Deployed

The subgraph is live and serves data for analytics and frontend applications.

## Endpoints

| Network | GraphQL Endpoint |
|---------|-----------------|
| ETC Mainnet | [`v2-graph.etcswap.org/subgraphs/name/etcswap/graphql`](https://v2-graph.etcswap.org/subgraphs/name/etcswap/graphql) |

## Contract References

### Ethereum Classic (Chain ID: 61)

| Contract | Address |
|----------|---------|
| Factory | [`0x0307cd3D7DA98A29e6Ed0D2137be386Ec1e4Bc9C`](https://etc.blockscout.com/address/0x0307cd3D7DA98A29e6Ed0D2137be386Ec1e4Bc9C) |
| WETC | [`0x1953cab0E5bFa6D4a9BaD6E05fD46C1CC6527a5a`](https://etc.blockscout.com/token/0x1953cab0E5bFa6D4a9BaD6E05fD46C1CC6527a5a) |
| USC | [`0xDE093684c796204224BC081f937aa059D903c52a`](https://etc.blockscout.com/token/0xDE093684c796204224BC081f937aa059D903c52a) |

## ETC-Specific Changes (etcswap branch)

- `src/mappings/pricing.ts` — WETC address and USD pricing via USC stablecoin
- Token pair references updated for ETC-native tokens

## Indexed Entities

- **EtcswapFactory** — Global protocol stats (pair count, total volume, total liquidity)
- **Token** — Per-token aggregated data (volume, liquidity, price derivations)
- **Pair** — Per-pair reserves, volume, transaction history
- **Transaction** — Individual swaps, mints, burns with amounts
- **User / LiquidityPosition** — LP tracking over time
- **PairDayData / TokenDayData** — Daily aggregated snapshots

## Example Query

```graphql
{
  etcswapFactories(first: 1) {
    pairCount
    totalVolumeUSD
    totalLiquidityUSD
  }
}
```

## Related Repos

- [v2-info](https://github.com/etcswap/v2-info) — Analytics frontend (consuming this subgraph)
- [v2-core](https://github.com/etcswap/v2-core) — Factory and Pair contracts
- [v2-interface](https://github.com/etcswap/v2-interface) — Trading frontend

## Local Development

```bash
yarn install
yarn codegen
yarn build
yarn deploy
```
