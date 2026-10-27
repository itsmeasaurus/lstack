---
name: typescript-best-practices
description: TypeScript rules for safer types. Use when reading or editing any .ts or .tsx file.
paths: ["**/*.ts", "**/*.tsx"]
user-invocable: false
---

# TypeScript best practices

Follow the existing style of the file first. Apply these where they fit.

- **Unions with a `kind` field** for things that have variants, so impossible states can't exist. Avoid objects full of optional fields.
- **Branded types** for IDs and other primitives that must not be mixed up, for example `type UserId = string & { readonly __brand: "UserId" }`. Create them only through a checking function (`isUserId(x): x is UserId`), never with `as`.
- **Make bad values impossible to build**: `[T, ...T[]]` for "at least one", a `start` plus `duration` instead of two dates that could be out of order. But keep `T[]` while that works without `!`, casts, or "should never happen" throws.
- **`unknown`, not `any`**, for data from outside (API responses, `JSON.parse`, env, files).
- **Schemas over hand-written checks**: if the repo uses a schema library (zod, valibot, etc.), define the schema and derive the type from it (`z.infer`).
- **No `as` casts** except right after validation. Prefer `satisfies` to check a value without losing its literal types.
- **Narrowing order**: `switch` on a discriminant > `in` > `typeof` / `instanceof` > type guard function > `as`.
- **Type guards must really check** what they claim. Name them `isX` / `hasX`. A guard that lies is worse than `as`.
- **Exhaustive switches**: in the `default` branch write `const _exhaustive: never = x;` so adding a new variant causes a compile error.
- **Validate at the edges**: parse incoming data once, where it enters (HTTP handler, config load, queue consumer), into a named type. Trust the type inside.
- **Reuse types**: reach for `Pick`, `Omit`, `Parameters`, `ReturnType`, `Awaited`, `typeof` before writing a new interface.
- **Object parameters** instead of long positional argument lists, except in very hot code.
- **Real tests**: don't mock what you can run locally. Mock only what you can't.
- **Structured logging** with enough context (like an ID) to debug. No `console.log` in shipped code.
