# Command Line

## npm -v

Check the npm version.

## npm init



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

