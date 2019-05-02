The remaining exercises will happen in this repo, schematics-workshop. Switch back to this repository and check out the appropriate branch for each exercise.

## Checkout branch

Checkout the `apply` branch:

```bash
npm run clean

git checkout -f apply
```

## Apply the files

Open the src/schematic-starter/index.ts file.

This exercise is similar to creating files with the `tree.create()` command, only here we're reading from a directory and optionally applying `Rules` against the template.

1. Use the `url()` function to retrieve the source from the `'./files'` directory.

```ts
const source = url("./files");
```

2. use the `apply()` function to apply rules (empty for now) and invoke it with the `context`

```ts
return apply(source, rules)(context);
```

## Execute with the Sandbox

```bash
npm test
```

You should have an `index.html` in the root of the `sandbox` folder. This file was read from the src/schematic-starter/files directory by the schematic executed in the sandbox.

Since the sandbox is version controlled, you can visually see the changes the schematic makes using your editor or git diff tool of choice.

### Bonus

1. Try adding a nested folder and files in the `src/schematics-starter/files` folder.
1. Use your version control system to see what files have changed. In the VSCode menu `View > SCM`
