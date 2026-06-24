# About

This branch (tanstack-query-sdk-flat-params-integration) is for reproducing, investigating, and potentially fixing [issue #3191](https://github.com/hey-api/hey-api/issues/3191).

A reproduction example has been added to the branch at `bug-tanstack-query-sdk-flat-params-integration`.

## Reproduction

To reproduce the issue, run the following, navigate to `bug-tanstack-query-sdk-flat-params-integration` and run the following commands:

```bash
cd examples/bug-tanstack-query-sdk-flat-params-integration
pnpm i
pnpm run openapi-ts
pnpm typecheck
```

You should see errors in `src/client/@tanstack/react-query.gen.ts` like this:

```
src/client/@tanstack/react-query.gen.ts:52:5 - error TS2322: Type '(fnOptions: Options<AddPetData>) => Promise<Pet | undefined>' is not assignable to type 'MutationFunction<Pet, Options<AddPetData>>'.
  Type 'Promise<Pet | undefined>' is not assignable to type 'Promise<Pet>'.
    Type 'Pet | undefined' is not assignable to type 'Pet'.
      Type 'undefined' is not assignable to type 'Pet'.

52     mutationFn: async (fnOptions) => {
       ~~~~~~~~~~

  ../../node_modules/.pnpm/@tanstack+query-core@5.73.3/node_modules/@tanstack/query-core/build/modern/hydration-p5rrYdPC.d.ts:1177:5 - The expected type comes from property 'mutationFn' which is declared here on type 'UseMutationOptions<Pet, Error, Options<AddPetData>, unknown>'
    1177     mutationFn?: MutationFunction<TData, TVariables>;
             ~~~~~~~~~~
```
