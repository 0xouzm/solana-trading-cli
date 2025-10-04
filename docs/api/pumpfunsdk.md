## Pump.fun SDK Helpers
Lightweight wrapper helpers and types for interacting with the Pump.fun program.

Entry: `src/pumpfunsdk/pumpdotfun-sdk/src/index.ts` re-exports core classes, types, and utils.

### Core
- `PROGRAM_ID`, `MPL_TOKEN_METADATA_PROGRAM_ID`
- `GLOBAL_ACCOUNT_SEED`, `MINT_AUTHORITY_SEED`, `BONDING_CURVE_SEED`, `METADATA_SEED`
- `DEFAULT_DECIMALS`
- `class PumpFunSDK` — high-level methods for create/buy/sell and event listeners
  - `createAndBuy(creator: Keypair, mint: Keypair, tokenMetadata: {...}, buyAmountSol: bigint, slippageBps?: bigint, priorityFees?)`
  - `buy(buyer: Keypair, mint: PublicKey, buyAmountSol: bigint, slippageBps?: bigint, priorityFees?)`
  - `sell(seller: Keypair, mint: PublicKey, sellTokenAmount: bigint, slippageBps?: bigint, priorityFees?)`
  - `getGlobalAccount()`, `getBondingCurveAccount(mint)`, PDA helpers, metadata helpers
  - Event APIs: `addEventListener(eventType, callback)` / `removeEventListener(eventId)`

Example:
```ts
import { PumpFunSDK, DEFAULT_DECIMALS } from "./src/pumpfunsdk/pumpdotfun-sdk/src";
import { wallet, connection } from "./src/helpers";
import { AnchorProvider } from "@coral-xyz/anchor";
const provider = new AnchorProvider(connection, { publicKey: wallet.publicKey } as any, { commitment: "finalized" });
const sdk = new PumpFunSDK(provider);
```

### Toolkit (`src/pumpfunsdk/pumpdotfun-sdk/src/tools.ts`)
High-level functions using `PumpFunSDK`:
- `createAndBuy(pathToMintKeypair: string, tokenMetadata: object, initialBuySolAmount: number)`
- `sell(mintPubKey: PublicKey, sellPercentage: number)`
- `buy(mintPubKey: PublicKey, solPerOrder: number)`

Example:
```ts
import { createAndBuy, buy, sell } from "./src/pumpfunsdk/pumpdotfun-sdk/src/tools";
await createAndBuy("/path/to/mint.json", { name: "MY", symbol: "MY", description: "..." }, 0.01);
```

### Types and events
- `types.ts`: `CreateTokenMetadata`, `TokenMetadata`, `CreateEvent`, `TradeEvent`, `CompleteEvent`, `SetParamsEvent`, `PriorityFee`, `TransactionResult`
- `events.ts`: conversion helpers `toCreateEvent`, `toTradeEvent`, `toCompleteEvent`, `toSetParamsEvent`

### Utility
- `util.ts`: commitment/finality constants, slippage calculators, tx builders (`sendTxToJito`, `sendTx`, `buildVersionedTx`, `getTxDetails`, key generation)

Notes:
- These helpers use the repo’s `wallet` and `connection` unless overridden.
