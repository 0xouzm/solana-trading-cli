## Transactions
Low-level transaction execution helpers.

### `src/transactions/simple_tx_executor.ts`
- `simple_executeAndConfirm(transaction: VersionedTransaction|Transaction, payer: Keypair, lastestBlockhash: BlockhashWithExpiryBlockHeight): Promise<{ confirmed: boolean, signature: string }>`

Example:
```ts
import { simple_executeAndConfirm } from "./src/transactions";
const latest = await connection.getLatestBlockhash("confirmed");
const { confirmed, signature } = await simple_executeAndConfirm(tx, wallet, latest);
```

### `src/transactions/jito_tips_tx_executor.ts`
- `getRandomValidator(): Promise<PublicKey>`
- `jito_executeAndConfirm(transaction: VersionedTransaction, payer: Keypair, lastestBlockhash: BlockhashWithExpiryBlockHeight, jitofee: number|string)`
- `jito_confirm(signature: string, latestBlockhash: BlockhashWithExpiryBlockHeight)`

Example:
```ts
import { jito_executeAndConfirm } from "./src/transactions";
const latest = await connection.getLatestBlockhash("confirmed");
const res = await jito_executeAndConfirm(tx, wallet, latest, jito_fee);
```

### `src/transactions/bloXroute_tips_tx_executor.ts`
- `CreateTraderAPITipTransaction(...)`
- `bloXroute_executeAndConfirm(transaction: VersionedTransaction, signers: Keypair[])`
