## gRPC Streaming (experimental)
Developer utilities for streaming Solana data and reacting to new tokens on Pump.fun or Raydium via Yellowstone gRPC.

### PF Sniper: `src/grpc_streaming_dev/grpc-pf-sniper/*`
- `streaming/pump.fun.ts`
  - `populateJitoLeaderArray()`
  - `waitAndSellAll(mintAddress: string, isJito: boolean)`
  - `streamAnyNewTokens(isAutoSell: boolean, sellAfterNumberBuys: number, isJito: boolean, n: number)`
  - `streamTargetNewToken(mintAddress: string, isAutoSell: boolean, sellAfterNumberBuys: number, isJito: boolean)`
- `streaming/grpc-requests-type.ts`: builders for `SubscribeRequest`
  - `createSubscribeNewTokenRequest(mintAddress?: string)`
  - `createSubscribeTokenRequest(mintAddress: string)`
  - `createSubscribeTokenInSnipeCacheRequest(snipedTokenList: string[])`
  - `createClearAllSubscriptionsRequest()`
- `streaming/utils.ts`
  - `handleSubscribe(stream, request)`

Usage example:
```ts
import { streamAnyNewTokens } from "./src/grpc_streaming_dev/grpc-pf-sniper/src/streaming/pump.fun";
await streamAnyNewTokens(true, 1, true, 3);
```

### Raydium sniper (dev): `src/grpc_streaming_dev/grpc-raydium-sniper/*`
- Buffer, constants, Jito bundle sender, token cache, and streaming listeners for OpenBook/Raydium. APIs are volatile.

Notes:
- These modules assume valid Yellowstone gRPC credentials and env vars (`GRPC_URL`, `GRPC_XTOKEN`).
- Treat as experimental; API may change.
