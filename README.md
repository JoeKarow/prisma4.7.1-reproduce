# Prisma 4.7.1 error reproduction

This is a pared-down version of our current schema. This error was introduced in `prisma@4.7.0` and still exists in `prisma@4.7.1` when the new `clientExtensions` feature is enabled.

Error message:

```bash
pnpm generate && tsc --noEmit

> prisma-error@1.0.0 generate /Users/joe/GitHub/InReach/prisma-error
> prisma generate

Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma

✔ Generated Prisma Client (4.7.1 | library) to ./node_modules/.pnpm/@prisma+client@4.7.1_prisma@4.7.1/node_modules/@prisma/client in 230ms
You can now start using Prisma Client in your code. Reference: https://pris.ly/d/client

import { PrismaClient } from '@prisma/client'
const prisma = new PrismaClient()

/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:99606
                throw e;
                ^

RangeError: Maximum call stack size exceeded
    at getResolvedMembersOrExportsOfSymbol (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:48886:53)
    at getMembersOfSymbol (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:48932:19)
    at isEmptyAnonymousObjectType (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:54984:60)
    at Object.some (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:663:25)
    at getNormalizedUnionOrIntersectionType (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:55142:44)
    at getNormalizedType (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:55128:48)
    at isRelatedTo (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:55440:30)
    at typeRelatedToEachType (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:55751:35)
    at unionOrIntersectionRelatedTo (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:55687:28)
    at structuredTypeRelatedToWorker (/Users/joe/Library/pnpm/global/5/.pnpm/typescript@4.9.3/node_modules/typescript/lib/tsc.js:56024:34)
```

Commenting out line 127 & lines 220-236 of `prisma/prisma.schema` (UserTitle model & relation field on User model) will not result in error.

```bash
pnpm generate && tsc --noEmit

> prisma-error@1.0.0 generate /Users/joe/GitHub/InReach/prisma-error
> prisma generate

Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma

✔ Generated Prisma Client (4.7.1 | library) to ./node_modules/.pnpm/@prisma+client@4.7.1_prisma@4.7.1/node_modules/@prisma/client in 237ms
You can now start using Prisma Client in your code. Reference: https://pris.ly/d/client

import { PrismaClient } from '@prisma/client'
const prisma = new PrismaClient()
```
