# Command Line(Update on 2022.04.18)

## npm -v

Check the npm version.

## npm init

`npm init <initializer>` can be used to set up a new or existing package.

```npm
npm init [--force|-f|--yes|-y|--scope]
```

When we use `npm init`, omitting the `<initializer>` , init will fall back to the legacy init behaviour, it will ask a bunch of questions, and then write a package for you, It will attempt to make reasonable guesses based on existing fields,dependencies and options selected.

If pass `-y|--yes`, it will skip the questionnaire altogether.

For more details, looking for [npm-init](https://docs.npmjs.com/cli/v8/commands/npm-init).

## npm install \<Module Name>

Install the module in current folder, you can only use this module under the current folder.

### Install specific module version

``` npm
npm install <module name>@<version>
//e.g
npm install webpack@4.43.0
```

### Flags

* -g: install the module globally, so you can use it in anywhere.
* -D/--save-dev: install the module in devDependencies, which won't be packed when deploying to production.
* -S/--save: default flag, install module in dependencies which will be packed when deploying to production.

## npm uninstall \<Module Name>

Uninstall the module in current folder.

### Flags

* -g: uninstall the module installed globally.

## npm list

Check modules and their versions which installed in current folder.

### Flags

* -g: check the modules and their versions which installed globally

## npm list \<Module Name>

Check module's version installed in the current folder.

### Flags

* -g: check modules's version installed globally.

