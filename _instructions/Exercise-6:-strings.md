## Checkout branch

Checkout the `strings` branch:

```bash
npm run clean

git checkout -f strings
```

## Add a prompt for the browserType

In the src/schematic-starter/schema.json file

1. Add a prompt for `browserType`

```json
"browserType": {
  "enum": ["netscape", "internetExplorer"],
  "description": "Supported browser",
  "default": "netscape",
  "x-prompt": "Select the supported browser"
}
```

## Add check for a missing `name` property

In the src/schematic-starter/index.ts file

1. Add a `name` guard and throw a `SchematicsException` if not found.

```ts
if (!_options.name) {
  throw new SchematicsException("Entity name is required");
}
```

## Add a debug statement

```ts
context.logger.debug(`adding files to ${path} dir`);
```

## Override the `browserType` property

Use the helper method provided to turn the prompt selection into a base64 string;

```ts
_options.browserType = getBase64Image(_options.browserType);
```

## Apply the template and move rules to the source files

```ts
return apply(url("./files"), [
  template({
    ...strings,
    ..._options
  }),
  move(path)
])(context);
```

## String interpolation

In the `src/schematic-starter/files/__name@dasherize__.component.html` file

1. Interpolate the `browserType` value.

```ts
<img width="300" alt="browser type" src="<%= browserType %>">
```

In the `src/schematic-starter/files/__name@dasherize__.component.ts` file

2. Interpolate the `selector`, `name` and `style` properties using the `dasherize` `classify` methods where appropriate.

```ts
selector: '<%= selector %>',
```

```ts
templateUrl: './<%= dasherize(name) %>.component.html',
styleUrls: ['./<%= dasherize(name) %>.component.<%= style %>']
```

```ts
export class <%= classify(name) %>Component implements OnInit {
```

## Execute with the Sandbox

```bash
npm test
```

You should have three new files added at sandbox/src/app/components/ with the `browserType`, `selector`, `name` and `style` properties correctly formatted.

### Bonus

- Try some of the other available string methods in the `.html` or `.ts` files,

`decamelize`, `dasherize`, `camelize`, `classify`, `underscore`, `capitalize`, `levenshtein`
