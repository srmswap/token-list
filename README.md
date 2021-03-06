# @solana/spl-token-registry

[![npm](https://img.shields.io/npm/v/@solana/spl-token-registry)](https://unpkg.com/@solana/spl-token-registry@latest/) [![GitHub license](https://img.shields.io/badge/license-APACHE-blue.svg)](https://github.com/solana-labs/token-list/blob/b3fa86b3fdd9c817139e38641d46c5a892542a52/LICENSE) 

Solana Token Registry is a package that allows application to query for list of tokens.
JSON schema for the tokens includes: name, symbol, logo and mint account address

## Installation

```bash
npm install @solana/spl-token-registry
```

```bash
yarn install @solana/spl-token-registry
```

## Examples

### Query available tokens

```typescript 

new TokenListProvider().resolve("mainnet-beta").then(tokens => {
  console.log(tokens);
});

```

### Render icon for token in React

```typescript jsx
import React, { useEffect, useState } from 'react';
import { TokenListProvider, KnownToken } from '@solana/spl-token-registry';


export const Icon = (props: { mint: string }) => {
  const [tokenMap, setTokenMap] = useState<Map<string, KnownToken>>(new Map());

  useEffect(() => {
    new TokenListProvider().resolve("mainnet-beta").then(tokens => {
      setTokenMap(tokens.reduce((map, item) => {
        map.set(item.mintAddress, item);
        return map;
      },new Map()));
    });
  }, [setTokenMap]);

  const token = tokenMap.get(props.mint);
  if (!token) return null;

  return (<img src={token.icon} />);

```

## Adding new token

Submit PR with changes to JSON file `src/tokens/<env>.json`
