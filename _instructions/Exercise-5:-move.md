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

LMA::

```json
{
  "$schema": "http://json-schema.org/schema",
  "id": "SchematicsStarter",
  "title": "Options Schema",
  "type": "object",
  "required": [],
  "additionalProperties": false,
  "properties": {
    "name": {
      "type": "string",
      "description": "Name of the componet",
      "default": "ng-conf",
      "x-prompt": "Enter the name of the component"
    }
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

LMA::

```json
{
  "$schema": "../node_modules/@angular-devkit/schematics/collection-schema.json",
  "schematics": {
    "schematic-starter": {
      "description": "A blank schematic.",
      "factory": "./schematic-starter/index#schematicStarter",
      "schema": "./schematic-starter/schema.json"
    },
    "ng-add": {
      "description": "Add SchematicStarter to an application.",
      "factory": "./schematic-starter/index#schematicStarter",
      "schema": "./schematic-starter/schema.json"
    }
  }
}
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

LMA::

```ts
import {
  Rule,
  SchematicContext,
  Tree,
  apply,
  url,
  template,
  move
} from "@angular-devkit/schematics";
import { strings } from "@angular-devkit/core";

// declare AddFilesInterface
interface AddFilesInterface {
  name: string;
}

export function schematicStarter(_options: AddFilesInterface): Rule {
  return (tree: Tree, context: SchematicContext) => {
    // todo: use the template() function and provide the strings and _options members
    const rules: Rule[] = [
      template({ ...strings, ..._options }),
      move("src/app/components")
    ];

    const source = url("./files");
    return apply(source, rules)(context);
  };
}
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
