`webpack dev server` wil run a web server on our locall and can automatically compile our code whenver it changes so that we can avoid useing `npm run build` every time when we want to see the output, meanwhile it allows live reloading.

# Basic use

```js
const webpack = require("webpack");
const WebpackDevServer = require("webpack-dev-server");
const webpackConfig = require("./webpack.config.js");

const compiler = webpack(webpackConfig);
const devServerOptions = {
  static: "./dist",
};

const devServer = new WebpackDevServer(devServerOptions, compiler);

devServer.startCallback(() => {
  console.log("start webpack dev server successfully");
});
```

In here, the `devServerOptions` is the basic config for `webpack-dev-server` , it tells `webpack-dev-sever` to serve the files from `./dist` directory on `localhost:8080`.

But `webpack-dev-server` won't generate output files into `dist` directory after compiling, instead, it keeps bundled files in memory and serves them as they are real files mounted at server's root path.