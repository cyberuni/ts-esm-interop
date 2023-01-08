## Test Configuration

```js
{
  "compilerOptions": {
    "esModuleInterop": true,
    "moduleResolution": "Node"
  }
}
```

The `esModuleInterop` tries to solve the very problem about `export =` and `export default`.

## Test Subjects

Depends on the test configuration, the way to consume a module are different.

In this section we describe each module and how they are consumed within this configuration.

## [assert](../../README.md#assert)

```ts
import assert from 'assert'
import { default as assert } from 'assert'
import * as assert from 'assert'
assert(true)
```

## [assertron@7](../../README.md#assertron7)

```ts
import assertron from 'assertron'
import { default as assertron } from 'assertron'
assertron.truthy(1)

import * as assertron from 'assertron'
assertron.default.truthy(1)
```

## [param-case@1](../../README.md#param-case1)

```ts
// export =
import paramCase from 'param-case'
import { default as paramCase } from 'param-case'
paramCase('hello world')

import * as paramCase from 'param-case'
paramCase.default('hello world')
```

## [cjs](../../README.md#cjs)

```ts
import m from 'cjs'
import { default as m } from 'cjs'
m(1)

import * as m from 'cjs'
m.default(1)
```

## [es-cjs](../../README.md#es-cjs)

```ts
import m from 'es-cjs'
import { default as m } from 'es-cjs'
m(1)

import * as m from 'es-cjs'
m.default(1)
```

## [esm-cjs](../../README.md#esm-cjs)

```ts
import m from 'esm-cjs'
import { default as m } from 'esm-cjs'
m(1)

import * as m from 'esm-cjs'
m.default(1)
```

## Legends

- 🟢: both compile and runtime are working correctly
- 🟡: for compile, it means there is an error, but can be suppressed (e.g. with `skipLibCheck`)\
  for runtime, it means the compile fails, but runtime is working
- 🔴: both compile and runtime fails
- ❌: compile success, but runtime fails. Potentially a TypeScript bug.
- ➖: invalid usage in this test configuration

Import Syntax:

- `default`: `import m from 'm'`
- `default as`: `import { default as m } from 'm'`
- `* as`: `import * as m from 'm'`

## Test Result

| module   | Package    | Type      | import: default as | import: default   | import: * as      |
| -------- | ---------- | --------- | ------------------ | ----------------- | ----------------- |
| CommonJS | assert     | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | ❌ not-fn          |
|          | assertron  | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | 🟢                 |
|          | param-case | 💻 Compile | 🟢                  | 🟢                 | 🔴 TS2497-e TS2339 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | 🟡                 |
|          | cjs        | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | 🟢                 |
|          | es-cjs     | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | 🟢                 |
|          | esm        | 💻 Compile | ➖                  | ➖                 | ➖                 |
|          |            | 🏃 Runtime | ➖                  | ➖                 | ➖                 |
|          | esm-cjs    | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | 🟢                 |
| ES*      | assert     | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | ❌ not-fn          |
|          | assertron  | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | ❌ not-fn           | ❌ not-fn          | ❌ not-fn          |
|          | param-case | 💻 Compile | 🟢                  | 🟢                 | 🔴 TS2497-a TS2339 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | 🟡                 |
|          | cjs        | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | ❌ not-fn           | ❌ not-fn          | ❌ not-fn          |
|          | es-cjs     | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | ❌ not-fn           | ❌ not-fn          | ❌ not-fn          |
|          | esm        | 💻 Compile | ➖                  | ➖                 | ➖                 |
|          |            | 🏃 Runtime | ➖                  | ➖                 | ➖                 |
|          | esm-cjs    | 💻 Compile | 🟢                  | 🟢                 | 🟢                 |
|          |            | 🏃 Runtime | 🟢                  | 🟢                 | 🟢                 |
| Node*    | assert     | 💻 Compile | ❌ to-cjs           | ❌ to-cjs          | ❌ to-cjs          |
|          |            | 🏃 Runtime | ❌ ref-err          | ❌ ref-err         | ❌ ref-err         |
|          | assertron  | 💻 Compile | ❌ to-cjs TS1259-t  | ❌ to-cjs TS1259-t | ❌ to-cjs TS1259-t |
|          |            | 🏃 Runtime | ❌ ref-err          | ❌ ref-err         | ❌ ref-err         |
|          | param-case | 💻 Compile | ❌ to-cjs           | ❌ to-cjs          | ❌ to-cjs          |
|          |            | 🏃 Runtime | ❌ ref-err          | ❌ ref-err         | ❌ ref-err         |
|          | cjs        | 💻 Compile | ❌ to-cjs           | ❌ to-cjs          | ❌ to-cjs          |
|          |            | 🏃 Runtime | ❌ ref-err          | ❌ ref-err         | ❌ ref-err         |
|          | es-cjs     | 💻 Compile | ❌ to-cjs           | ❌ to-cjs          | ❌ to-cjs          |
|          |            | 🏃 Runtime | ❌ ref-err          | ❌ ref-err         | ❌ ref-err         |
|          | esm        | 💻 Compile | ➖                  | ➖                 | ➖                 |
|          |            | 🏃 Runtime | ➖                  | ➖                 | ➖                 |
|          | esm-cjs    | 💻 Compile | ❌ to-cjs           | ❌ to-cjs          | ❌ to-cjs          |
|          |            | 🏃 Runtime | ❌ ref-err          | ❌ ref-err         | ❌ ref-err         |

- to-cjs: Code are compiled to CJS incorrectly
- TS1259-e: `TS1259: needs esModuleInterop`
- TS1259-a: `TS1259: needs allowSyntheticDefaultImports`
- TS1259-t: (transient) `TS1259: ...node_modules/assertion-error can only be default-imported using the 'allowSyntheticDefaultImports' flag`\
  `export = AssertionError`\
  `This module is declared with 'export =', and can only be used with a default import when using the 'allowSyntheticDefaultImports' flag.`
- TS2339: `TS2339: Property 'default' does not exist on type '(value: string, locale?: string | undefined) => string'`
- TS2497-a: `TS2497: needs allowSyntheticDefaultImports and referencing its default export`
- TS2497-e: `TS2497: needs esModuleInterop and referencing its default export`
- not-fn: `TypeError: not a function`
- ref-err: `ReferenceError: exports is not defined in ES module scope` (due to to-cjs)

## Conclusion

- `module: CommonJS` works on most cases.
  This is expected as that is the majority case for many years.
  - for `* as assert` case, while `esModuleInterop` tries to solve that problem,
    and the consumer should use the other forms. The compiler passing it is a bug IMO.
- ❌ `module: ES*` fails with CJS is suprising, and if the test is correct, it's disturbing.
- ❌ `module: Node*` compiled to CJS incorrectly
