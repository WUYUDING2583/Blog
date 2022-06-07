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

In here, the `devServerOptions` is the basic config for `webpack-dev-server` , it tells `webpack-dev-sever` to serve the static files from `./dist` directory on `localhost:8080`.

But `webpack-dev-server` won't generate output files into `dist` directory after compiling, instead, it keeps bundled files in memory and serves them as if they are real files mounted at server's root path.

When we open `localhost:8080` in browser while we don't provide any static files e.g. **index.html**, the server will get `404` error because it cannot find any file `webpack dev server` can serve. Thus we need to provide our static files in the declared `static directory`. If the `static` configuration is not provided, the default value of it is `public directory`.

# API

## start

This API instructs `webpack-dev-server` instance to start the server.

```js
const webpack = require("webpack");
const WebpackDevServer = require("webpack-dev-server");
const webpackConfig = require("./webpack.config.js");

const compiler = webpack(webpackConfig);
const devServerOptions = {
  static: "./dist",
};

const devServer = new WebpackDevServer(devServerOptions, compiler);

const runServer=async ()=>{
  console.log("Starting server...");
  await devServer.start();
}

runServer();
```

## startCallback(callback)

This API instructs `webpack-dev-server` instance to start the server and run the callback function.

```js
const webpack=require("webpack");
const WebpackDevServer=require("webpack-dev-server");
const webpackConfig=require("./webpack.config.js");

const compiler=webpack(webpackConfig);
const devServerOptions={
  static: "./dist",
}
const devServer=new WebpackDevServer(devServerOptions,compiler);

devServer.startCallback(()=>{
  console.log("Successfully started server on localhost:8080");
})
```

## stop

This API instructs `webpack-dev-server` instance to stop the server.

```js
const webpack = require("webpack");
const WebpackDevServer = require("webpack-dev-server");
const webpackConfig = require("./webpack.config.js");

const compiler = webpack(webpackConfig);
const devServerOptions = {
  static: "./dist",
};

const devServer = new WebpackDevServer(devServerOptions, compiler);

const runServer=async ()=>{
  console.log("Starting server...");
  await devServer.start();
}

const stopServer=async ()=>{
  console.log('Stopping server...');
  await devServer.stop();
}

runServer();
setTimeout(stopServer,5000);
```

## stopCallback(callback)

This API instructs `webpack-dev-server` instance to stop the server and then run the callback function.

```js
const webpack=require("webpack");
const WebpackDevServer=require("webpack-dev-server");
const webpackConfig=require("./webpack.config.js");

const compiler=webpack(webpackConfig);
const devServerOptions={
  static: "./dist",
}
const devServer=new WebpackDevServer(devServerOptions,compiler);

devServer.startCallback(()=>{
  console.log("Successfully started server on localhost:8080");
})

const stopServer=()=>{
  devServer.stopCallback(()=>{
    console.log("Server stopped");
  });
}

setTimeout(stopServer,5000);
```

# Configuration

## static

