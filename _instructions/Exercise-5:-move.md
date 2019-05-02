## Checkout branch

Checkout the `move` branch:

```bash
npm run clean

git checkout -f move
```

## Add a prompt for the component name

In the src/schematic-starter/schema.json file:

1. Add a prompt for `name`

```json
"properties": {
  "name": {
    "type": "string",
    "description": "Name of the componet",
    "default": "ng-conf",
    "x-prompt": "Enter the name of the component"
  }
}
```

## Wire up the schema to the schematics CLI

In the src/collection.json file:

1. Add the `schema` property to each `schematics` entry under the `factory` property.

```json
"factory": "./schematic-starter/index#schematicStarter",
"schema": "./schematic-starter/schema.json"
```

## Add options interface

In src/schematic-starter/index.ts file:

1. Create an interface called `AddFilesInterface` with a `name: string` entry.
1. Replace the `any` type for the `_options` function argument in the `schematicStarter` method.

## Add the template method for interpolation

In src/schematic-starter/index.ts file:

1. Use the `template()` function and provide the `strings` and `_options` members

```ts
const rules: Rule[] = [template({ ...strings, ..._options })];
```

2. Add a second Rule that tells the schematic where to place the file

```ts
const rules: Rule[] = [
  template({ ...strings, ..._options }),
  move("src/app/components")
];
```

## Add files to the files directory

In the src/schematic-starter/files directory:

1. Remove the index.html file
1. Add the following files

```
__name@dasherize__.component.ts
__name@dasherize__.component.css
__name@dasherize__.component.html
```

## Execute with the Sandbox

```bash
npm test
```

You should have 3 files added to the sandbox with the filename you provided to the CLI prompt in sandbox/src/app/components.
