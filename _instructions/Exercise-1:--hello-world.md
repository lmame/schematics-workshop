## Create a new schematics project using the CLI

The Schematics CLI uses the following command pattern for executing schematics:

`schematics <directory>:<schematic> [options]`

1. run the following command outside of the schematics-workshop repo you cloned earlier. This will generate a new schematic project.

```bash
schematics blank --name=hello-world
```

## Create hello-world file

1. `cd hello-world` and open the project
2. open the src/hello-world/index.ts file
3. use the `tree.create()` method to create a new `hello-world.html` file with the contents “Hello World!”.

```ts
return (tree: Tree, _context: SchematicContext) => {
  return tree.create("foo.html", "<h1>Hello World!</h1>");
};
```

## Build the project

```bash
npm run build
```

## Execute the hello-world schematic using the CLI

```bash
schematics .:hello-world --dry-run=false
```

You should have a file names foo.html in the root directory with the contents `<h1>hello</h1>`
