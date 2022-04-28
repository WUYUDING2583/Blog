# Package.json(Update on 2022.04.17)

```json
{
  "name": "Blog",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {},
	"devDependencies": {
    "webpack": "^4.43.0",
    "webpack-cli": "^3.3.12"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
}
```

## name

The name of package.

## version

The version of package.

## description

The description of package.

## main

It specifies the program entry file. It will load this file when we use `require(<Module Name>)`.

Its **default value** is the `index.js` in module's root folder.

## scripts

This property supports a number of built-in scripts and their preset life cycle event as well as arbitrary scripts.

These all can be executed by running `npm run-script <stage>` or `npm run <stage>` for shot.

Pre and post commands with the matching name will be executed as well (e.g. `premyscript`, `myscript` and `postmyscript`)

### Pre&Post script

To create a pre&post script for any script defined in `scripts` section, simply create another script with the matching name and add `pre` or  `post` to the begining of them.

```json
{
  "scripts": {
    "precompress": "{{ executes BEFORE the `compress` script }}",
    "compress": "{{ run command to compress files }}",
    "postcompress": "{{ executes AFTER `compress` script }}"
  }
}
```

## dependencies

The dependency list, which contains  packages will be used in production.

## devDependencies

The development dependency list, which contains packages only used in development.

## Package version

* 10.4.4: Install the particular version **10.4.4**.
* ^10.4.4: Install the latest version in **10.x.x**.
* ~10.4.4: Install the latest version in **10.0.x**.

```json
"devDependencies": {
    "autoprefixer": "10.4.4",
    "clean-webpack-plugin": "~4.0.0",
    "css-loader": "^5.0.1"
}
```

## browserslist

Define the browser that can support the frontend project by **queries**.

For more queries can be found in [Browserslist's GitHub repository](https://github.com/browserslist/browserslist).

```json
{
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
}
//or 
{
  "browserslist": {
     "last 1 chrome version",
     "last 1 firefox version",
     "last 1 safari version"
  },
}
```

