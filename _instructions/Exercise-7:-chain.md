## Checkout branch

Checkout the `chain` branch:

```bash
npm run clean

git checkout -f chain
```

## Chain multiple rules into a single rule.

In the src/schematic-starter/index.ts file:

1. In the main function, return the `chain` method and include the `addFiles` `Rule` function. Invoke with the tree and context to return a `Tree`.

```ts
return chain([addFiles(_options)])(tree, _context);
```

## Refactor return type to use `mergeWith`

In the `addFiles` helper function:

1. Use `mergeWith` to return the source files and accompanying `Rule`'s. With `mergeWith`, you can merge an input tree with the source passed in returning a `Rule`

```ts
const templateSource = apply(url("./files"), [
  template({
    ...strings,
    ..._options
  }),
  move(path)
]);

return mergeWith(templateSource);
```

## Execute with the Sandbox

```bash
npm test
```

You should have the three component files added to the sandbox at sandbox/src/app/components.

## Extend another schematic

In the chain method add another input to execute an external schematic:

example: `externalSchematic('@schuchard/prettier', 'add', {})`

```ts
return chain([
  addFiles(_options),
  externalSchematic("@schuchard/prettier", "add", {})
])(tree, _context);
```

## Execute with the Sandbox

```bash
npm test
```

You should have added the files and setup Prettier.

### Bonus - Run the sandbox

1. Open the sandbox/src/app/app.module.ts file and add the new component to the module declarations.
1. Open the sandbox/src/app/app.component.html file and replace the HTML with the new component selector.

If you choose the default name prompt you would use `NgConfComponent` and `<app-ng-conf></app-ng-conf>` for the above steps.

3. `cd sandbox`
4. `npm start`
