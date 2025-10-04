## Meteora DLMM
Helpers for Meteora DLMM pools for price and swaps.

Entry: `src/meteora/index.ts` re-exports helpers and pool ops.

### Price utilities (`src/meteora/fetch-price.ts`)
- `getCurrentPriceInSOL(tokenAddress: string)`
- `getCurrentSolPrice()`
- `getCurrentPriceInUSD(tokenAddress: string)`

### Pool utilities (`src/meteora/Pool/fetch-pool.ts`)
- `fetchDLMMPoolId(tokenAddress: string)`
- `fetchDLMMPool(tokenAddress: string)`

### Swap (`src/meteora/Pool/swap.ts`)
- `swap(...)` — programmatic swap via DLMM pools

### Buy/Sell helpers
- `buy(token_address: string, buyAmountInSOL: number)` (`src/meteora/buy_helper.ts`)
- `sell(token_address: string, sell_percentage: number)` (`src/meteora/sell_helper.ts`)

### Token filters (`src/meteora/token-filters/*`)
- `getCurrentSolInPool(token_address: string)`
- `getLastNDayVolume(tokenAddress: string, n: number)` / `getDayVolume` / `getWeekVolume` / `getMonthVolume`
- `getCurrentMarketCap(tokenAddress: string)`

### Constants (`src/meteora/constants.ts`)
- `PROGRAM_ID`, and common mint constants: `wsol`, `usdc`, `usdt`

Example:
```ts
import { fetchDLMMPoolId } from "./src/meteora";
const poolId = await fetchDLMMPoolId("<TOKEN_MINT>");
```
