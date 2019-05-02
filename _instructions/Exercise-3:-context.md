## Use SchematicContext.logger

1. Define a new constant variable named `logger` that is a reference to the `SchematicContext.logger` instance.
2. Use the `logger.debug()` method
3. Use the `logger.info()` method
4. Use the `logger.warn()` method
5. Use the `logger.error()` method

For example:

```typescript
export function schematicStarter(_options: any): Rule {
  return (tree: Tree, _context: SchematicContext) => {
    const logger = _context.logger;

    logger.debug("This is a debug message");

    return tree;
  };
}
```

LMA::

```ts
// You don't have to export the function as default. You can also have more than one rule factory
// per file.
interface HelloWorldOptions {
  name: string;
  fileExtension: string;
}

export function helloWorld(_options: HelloWorldOptions): Rule {
  // LMA:: Original code
  // return (tree: Tree, _context: SchematicContext) => {
  //   return tree;
  // };

  return (tree: Tree, _context: SchematicContext) => {
    // return tree.create("foo.html", "<h1>Hello World ${_options.name}!</h1>");

    const logger = _context.logger;

    logger.debug("This is a debug message");

    return tree.create(
      `${_options.name}.${_options.fileExtension}`,
      `<p>Hi, ${_options.name}!<p>`
    );
  };
}
```

## Build the project

```bash
npm run build
```

## Execute the hello-world schematic using the CLI

```bash
schematics .:hello-world --dry-run=false
```

You should see the `info`, `warn`, and `error` messages print out.

### Bonus

- Execute the `schematics` command by itself for a list of additional options
- Did the `debug` logger not print out? Run the schematic with with the verbose flag

```bash
schematics .:hello-world --dry-run=false --verbose
```
