# Configuration File (Update at 2022.04.27)

The default webpack configuration file name is `webpack.config.js` which is put in root folder.

Below is what this config file looks like:

```js
const path = require("path");
const htmlwebpackplugin = require("html-webpack-plugin");
const { CleanWebpackPlugin } = require("clean-webpack-plugin");
const minicss = require("mini-css-extract-plugin");
module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "./dist"), 
    filename: "[name].js",
  },
  mode: "development", //none | development | production
  resolveLoader: { modules: ["node_modules", "./loaders"] },
  module: {
    rules: [
      {
        test: /\.css$/, 
        use: ["style-loader", "css-loader"], 
      },
    ],
  },
  plugins: [
    new htmlwebpackplugin({
      template: "./src/index.html",
      filename: "index.html",
    }),
    new CleanWebpackPlugin(),
    new minicss({ filename: "style/index.css" }), 
  ],
};


```

# Entry

An **entry point** indicates the module that webpack will use to build its dependency graph. 

The default value of it is `./src/index.js`

```js
module.exports = {
  entry: './path/to/my/entry/file.js',
};
```

# Output

The output defines where webpack emit the bundles it creates and how to name it.

The main output file emit in `./dist/main.js` and other files to `./dist` folder.

`output.path` tell webpack the emit folder and its value is the absolute path of project.

`output.filename` tell webpack how to name the main bundles it creates.

```js
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js',
  },
};
```

# Loaders

By default, webpack can only work with `javascript` and `josn` files.

Loaders can allow webpack to process other type files and convert them into the valid module that can be used by our application and add it into dependency graph.

In order to use loaders, we need to config it in `module.rules`, and its value type is an **array**.

Loader configuration has two properties:

1. **test**: it defines which type of file should be converted.
2. **use**: it tells webpack use which loader to proceed the convert work.

In the example below, it tells webpack to use `raw-loader` to convert `.txt` files into the module that webpack can work with.

```js
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js',
  },
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
}; 
```

# Plugins

Plugins perform a wide range of tasks like bundle optimisation, assets management and injection of environment variables.

In order to use plugins, we should use `require()` to import the plugin and add it into the `plugins` array. As we can use the plugin multiple time, we need to create an **instance** of plugin.

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
  plugins: [new HtmlWebpackPlugin({ template: './src/index.html' })],
};
```

# Mode

The mode indicates which environment webpck should bundle. In different environments, webpack will enable different built-in optimisations.

Its value is either `development`, `production` or `none`.

```js
module.exports = {
  mode: 'production',
};
```

 

