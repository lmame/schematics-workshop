## Create a prompt in collection.json

1. Create a schema.json file at src/hello-world/schema.json.
2. Add a new `properties` top-level property.
3. Within that object, define a `name` property.
4. Set the `type` property value to `string`.
5. Provide a `description` property and value.
6. Provide the prompt text via the `x-prompt` property.

Here is an example of a string prompt:

```json
{
  "properties": {
    "name": {
      "type": "string",
      "description": "The name of the person to 👋 to.",
      "x-prompt": "What is the name of the person you want to say hi to?"
    }
  }
}
```

Next, add an `enum` prompt such as the one below

```json
{
  "properties": {
    "fileExtension": {
      "enum": ["ts", "html", "css", "spec.ts"],
      "description": "The file extension type",
      "default": "ts",
      "x-prompt": "Select a file type extension"
    }
  }
}
```

## Connect the Schematic Schema

In order utilize prompts, you need tell the CLI which schema to use.

1. Open the src/collection.json file and under `factory` add a `schema` property that points the the schema file you just edited.

```json
"factory": "./hello-world/index#helloWorld",
"schema": "./hello-world/schema.json"
```

## Define an Interface

1. Open the src/hello-world/index.ts file and define a new `HelloWorldOptions` interface.
1. The interface should have `name` and `fileExtension` members that are both of type `string`.
1. Modify the `helloWorld` function to replace the `any` type for the `_options` argument with the new `HelloWorldOptions` interface.

## Modify the tree.create method

1. Read the prompt value from the `_options` and interpolate the values in the file name and content arguments to `tree.create()`

```ts
return tree.create(
  `${_options.name}.${_options.fileExtension}`,
  `<p>Hi, ${_options.name}!<p>`
);
```

## Build the project

```bash
npm run build
```

## Execute the hello-world schematic using the CLI

```bash
schematics .:hello-world --dry-run=false
```

You should see a file add to the root directory with the `name` and `fileExtension` type you entered.
