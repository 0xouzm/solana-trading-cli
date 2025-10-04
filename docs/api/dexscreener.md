## Dexscreener
Utilities to fetch token and pair insights from Dexscreener.

### Exports (`src/dexscreener/info.ts`)
- `getInfoFromDexscreener(tokenAddress: string): Promise<{
  pairAge: string;
  name: string;
  address: string;
  priceInUSD: number;
  marketCap: number;
  dexscreenerURL: string;
  twitterURL: string;
  telegramURL: string;
  websiteURL: string;
  buyers5m: number; buyers1h: number; buyers6h: number; buyers24h: number;
  volume5m: number; volume1h: number; volume6h: number; volume24h: number;
  liquidityInSOL: number; poolId: string;
}>`

Example:
```ts
import { getInfoFromDexscreener } from "./src/dexscreener";
const info = await getInfoFromDexscreener("<TOKEN_MINT>");
console.log(info.priceInUSD, info.marketCap, info.poolId);
```
