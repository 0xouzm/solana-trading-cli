## Jupiter
High-level swap helpers and utilities to interact with Jupiter v6 quote/swap API.

Entry: `src/jupiter/index.ts` re-exports `swap/*` helpers.

### Swap helpers (`src/jupiter/swap/swap-helper.ts`)
- `getQuote(tokenToSell: string, tokenToBuy: string, convertedAmountOfTokenOut: number, slippage: number)`
- `getSwapTransaction(quoteResponse: any, wallet_pubKey: string)`
- `convertToInteger(amount: number, decimals: number)`
- `finalizeTransaction(swapTransaction: string)` → `{ confirmed, signature }`
- `swap(tokenToSell: string, tokenToBuy: string, amountTokenOut: number, slippage: number)`

Example:
```ts
import { swap } from "./src/jupiter";
const WSOL = "So11111111111111111111111111111111111111112";
await swap(WSOL, "<TOKEN_MINT>", 0.01, 100); // 1% slippage
```

### Buy helper (`src/jupiter/swap/buy-helper.ts`)
- `buy(tokenToBuy: string, amountTokenOut: number, slippage: number)`

Example:
```ts
import { buy as jupBuy } from "./src/jupiter";
await jupBuy("<TOKEN_MINT>", 0.015, 100);
```

### Sell helper (`src/jupiter/swap/sell-helper.ts`)
- `sell(tokenToSell: string, amountOfTokenToSell: number, slippage: number)`

Example:
```ts
import { sell as jupSell } from "./src/jupiter";
await jupSell("<TOKEN_MINT>", 0.000025, 100);
```
