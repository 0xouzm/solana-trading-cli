## Orca (Whirlpools)
Helpers around Orca Whirlpools SDK for price and swaps.

Entry: `src/orca/index.ts` re-exports `Pool/*` and helpers.

### Price utilities (`src/orca/fetch-price.ts`)
- `getCurrentPriceInSOL(tokenAddress: string)`
- `getCurrentSolPrice()`
- `getCurrentPriceInUSD(tokenAddress: string)`

### Pool utilities (`src/orca/Pool/fetch-pool.ts`)
- `fetchWhirlPoolId(tokenAddress: string)`
- `fetchWhirlPool(tokenAddress: string)`

### Swap (`src/orca/Pool/swap.ts`)
- `swap(...)` — programmatic swap using Whirlpools

### Buy/Sell helpers
- `buy(token_address: string, buyAmountInSOL: number)` (`src/orca/buy_helper.ts`)
- `sell(token_address: string, sell_percentage: number)` (`src/orca/sell_helper.ts`)

### Constants (`src/orca/constants.ts`)
- `PROGRAM_ID`, pool configs, and common mints: `wsol`, `usdc`, `usdt`, plus token metadata objects and `tick_spacing`.

Example:
```ts
import { getCurrentPriceInUSD } from "./src/orca";
const price = await getCurrentPriceInUSD("<TOKEN_MINT>");
```
