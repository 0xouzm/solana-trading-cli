## Helpers
Utility functions and configuration for wallets, RPC connections, transactions, SPL tokens, logging, and environment management.

### Config (`src/helpers/config.ts`)
Exports common configuration and initialized clients.
- `loadKeypairFromFile(filename: string): Keypair`
- `jito_fee: any` — string/number from `JITO_FEE`
- `shyft_api_key: string | undefined`
- `wallet: Keypair` — constructed from `PRIVATE_KEY`
- `private_key: string | undefined`
- `dev_endpoint: string`
- `main_endpoint: string`
- `bloXRoute_auth_header: string | undefined`
- `bloXroute_fee: any`
- `smart_money_wallet: string | undefined`
- `connection: Connection` — mainnet
- `dev_connection: Connection` — devnet
- `PROGRAMIDS`, `RAYDIUM_MAINNET_API`, `makeTxVersion`, `_ENDPOINT`, `addLookupTableInfo`
- `DEFAULT_TOKEN: { SOL, WSOL, USDC }`
- `wsol: string` — WSOL mint address

Example:
```ts
import { connection, wallet, jito_fee, wsol } from "./src/helpers";
```

Environment setup: ensure `src/helpers/.env` exists with keys from `src/helpers/.env.example`.

### Logger (`src/helpers/logger.ts`)
- `logger` — Pino logger instance, used across modules.

### Generic utilities (`src/helpers/utils.ts`)
- `TOKEN_PROGRAM_ID: PublicKey`
- `retrieveEnvVariable(name: string, logger: Logger): string` — reads a required env var (exits if missing)
- `getKeypairByJsonPath(path: string): Keypair` — reads a keypair JSON array
- `printSOLBalance(connection, pubKey, info?)`
- `getSPLBalance(connection, mint, pubKey, allowOffCurve?): Promise<number>`
- `printSPLBalance(connection, mint, user, info?)`
- `retriveWalletState(walletAddress: string): Promise<Record<string, number>>`

Examples:
```ts
import { printSOLBalance, getSPLBalance } from "./src/helpers";
await printSOLBalance(connection, wallet.publicKey, "Master wallet");
const balance = await getSPLBalance(connection, new PublicKey(mint), wallet.publicKey);
```

### Token/account helpers (`src/helpers/check_balance.ts`)
- `checkBalanceByAddress(address: string, connection: Connection): Promise<number>`
- `getSPLTokenBalance(connection: Connection, tokenMint: PublicKey, owner: PublicKey): Promise<number>`

### Token metadata and transactions (`src/helpers/util.ts`)
- `getTokenMetadata(address: string): Promise<{ tokenName?: string; tokenSymbol?: string }>`
- `sendTx(connection: Connection, payer: Keypair, txs: (VersionedTransaction|Transaction)[], options): Promise<string[]>`
- `getWalletTokenAccount(connection: Connection, wallet: PublicKey)`
- `buildAndSendTx(innerSimpleV0Transaction: any, options: any)` — builds V0 tx with priority fees and sends
- `sleepTime(ms: number)` / `sleep(ms: number)`
- `loadOrCreateKeypair_wallet(filepath: string): Promise<Keypair>`
- `isBlockhashExpired(lastValidBlockHeight: number): Promise<boolean>`
- `checkTx(txId: string): Promise<boolean>`
- `getDecimals(mintAddress: PublicKey): Promise<number>`

Example:
```ts
import { buildAndSendTx } from "./src/helpers";
const txids = await buildAndSendTx(innerTxs, { skipPreflight: true });
```

### WSOL utilities
`src/helpers/wrap_sol.ts`
- `wrap_sol(amount: number): Promise<void>` — wraps SOL into WSOL ATA via transfer + sync, sends via Jito helper
- `check_wsol_balance(wSolAta: PublicKey): Promise<void>`
- `main(): Promise<void>` — CLI entrypoint

`src/helpers/unwrap_sol.ts`
- `unwrapSol(): Promise<void>` — closes WSOL ATA, returns SOL

CLI usage examples:
```bash
# Wrap 0.05 SOL (CLI)
ts-node src/helpers/wrap_sol.ts --size 0.05
# Unwrap (CLI)
ts-node src/helpers/unwrap_sol.ts
```
Programmatic example:
```ts
import { wrap_sol, unwrapSol } from "./src/helpers";
await wrap_sol(0.05);
await unwrapSol();
```
