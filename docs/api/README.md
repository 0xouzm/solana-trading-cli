## Solana Trading CLI — API Reference

This reference documents all public APIs exported by the repository: functions, constants, and modules across Raydium, Jupiter, Orca, Meteora, helpers, transactions, Dexscreener utilities, Pump.fun SDK helpers, and experimental gRPC streaming utilities.

### Prerequisites
- Node: 22.2.0 (per `package.json` engines)
- TypeScript: 5.5+
- Environment variables: create `src/helpers/.env` based on `src/helpers/.env.example`

Example `.env` (fill values):
```ini
PRIVATE_KEY=...
MAINNET_ENDPOINT=...
DEVNET_ENDPOINT=...
WS_MAINNET_ENDPOINT=...
JITO_FEE="0.0001"
BLOXROUTE_FEE=0.001
# Optional gRPC/pump settings...
```

### Usage pattern
Import directly from module entrypoints under `src/` (internal usage):
```ts
import { buy as raydiumBuy } from "./src/raydium";
import { buy as jupiterBuy } from "./src/jupiter";
import { wrap_sol, unwrapSol } from "./src/helpers";
```

Initialize your wallet and connections via `src/helpers/config` or use the provided `connection` and `wallet` exports.

### Modules
- [Helpers](./helpers.md)
- [Dexscreener](./dexscreener.md)
- [Transactions](./transactions.md)
- [Jupiter](./jupiter.md)
- [Raydium](./raydium.md)
- [Orca](./orca.md)
- [Meteora](./meteora.md)
- [Pump.fun SDK](./pumpfunsdk.md)
- [gRPC Streaming (experimental)](./grpc_dev.md)

Notes:
- Some helpers are CLI-oriented (e.g., `wrap_sol.ts`, `unwrap_sol.ts`) but remain importable.
- The `src/utils/index.ts` re-exports most of `src/helpers` utilities for convenience.
