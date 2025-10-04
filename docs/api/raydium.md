## Raydium
Raydium AMM integrations for swaps, pool ops, and analytics.

Entry: `src/raydium/index.ts` re-exports helpers from submodules.

### Swap (`src/raydium/Pool/swap.ts`)
- `swap(side: "buy"|"sell", tokenAddr: string, buy_AmountOfSol: number, sell_PercentageOfToken: number, payer_wallet: Keypair, usage: "trade"|"volume")`
  - Executes swap via Raydium AMM. When `usage === "volume"`, returns inner transaction for batching.
- `swapForVolume(tokenAddr: string, sol_per_order: number)`
  - Composes a buy and sell to generate volume.

Examples:
```ts
import { swap, swapForVolume } from "./src/raydium";
await swap("buy", "<TOKEN_MINT>", 0.05, -1, wallet, "trade");
await swapForVolume("<TOKEN_MINT>", 0.01);
```

### Buy/Sell helpers
`src/raydium/buy_helper.ts`
- `buy(side: string, address: string, no_of_sol: number, payer: Keypair)`
- `get_buy_transaction(side: string, tokenAddr: string, buy_AmountOfSol: number, payer_wallet: Keypair)`

`src/raydium/sell_helper.ts`
- `sell(side: string, address: string, sell_percentage: number, payer: Keypair)`
- `get_sell_transaction(side: string, tokenAddr: string, payer_wallet: Keypair)`

### Price utilities (`src/raydium/fetch-price.ts`)
- `getCurrentPriceInSOL(tokenAddress: string)`
- `getCurrentSolPrice()`
- `getCurrentPriceInUSD(tokenAddress: string)`

### Pool discovery (`src/raydium/Pool/fetch_pool.ts`)
- `fetchAMMPoolId(tokenAddress: string)`
- `fetchAMMPoolIdByMintPair(mint1: string, mint2: string)`
- `fetchLPToken(tokenAddress: string)`

### Pool utils (`src/raydium/Pool/formatAmmKeysById.ts`)
- `formatAmmKeysById_swap(id: PublicKey)`
- `formatAmmKeysById_pool(id: PublicKey)`
- `formatAmmKeysById_swap_1(id: PublicKey)`
- `fetchPoolInfo(poolKeys: any, poolId: PublicKey)`

### Liquidity ops
- `ammAddLiquidity(input: any)` / `ammAddLiquidityHelper(input: any)` (`src/raydium/Pool/add_pool.ts`)
- `ammRemoveLiquidity(input: any)` / `ammRemoveLiquidityHelper(input: any)` (`src/raydium/Pool/remove_pool.ts`)

### Token filters (`src/raydium/token-filters/*`)
- `getLPBurnPercentage(tokenAddress: string)`
- `getCurrentSolInPool(tokenAddress: string)`
- `getDayVolume(tokenAddress: string)` / `getWeekVolume` / `getMonthVolume`
- `getCurrentMarketCap(tokenAddress: string)`

### Constants (`src/raydium/constants.ts`)
- `wsol`, `usdc`, `usdt`
