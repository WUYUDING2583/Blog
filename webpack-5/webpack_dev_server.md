`webpack dev server` wil run a web server on our locall and can automatically compile our code whenver it changes so that we can avoid useing `npm run build` every time when we want to see the output, meanwhile it allows live reloading.

# Basic Usage

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



# QA

## webpack dev server cannot reload when change html without insert the script

### Question

 When we provide a template html file for webpack dev server without using `html-webpack-plugin`, webpack dev server still can serve this template file.

When we manually insert the bundled file, webpack dev server can live reload the page when we change the code no matter in js file or html file. See code below:

webpack.config.js

```js
const path = require("path");
const appDirectory = process.cwd();
module.exports = {
  mode: "development",
  entry: { index: path.resolve(appDirectory, "src/index.js") },
  output: {
    filename: "[name].bundle.js",
    path: path.resolve("dist"),
    clean: true, //clean the output directory before generate bundles
  },
};

```

start.js

```js
const webpack = require("webpack");
const WebpackDevServer = require("webpack-dev-server");
const chalk = require("chalk");
const path = require("path");
const webpackConfig = require("../webpack.config");

let compiler;
try {
  compiler = webpack(webpackConfig);
} catch (err) {
  console.log(err.message || err);
}

const serverConfig = {
  port: 3001, //set the port to 3001
  // open: true, // open browser after compiling finish
};

const devServer = new WebpackDevServer(serverConfig, compiler);
devServer.startCallback(() => {
  console.log(chalk.blue("Start server successfully http://localhost:3001"));
});

```

index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>mini-react</title>
    <script src="index.bundle.js"></script>
  </head>
  <body>
    <div id="root">asaaasssssaaf</div>
  </body>
</html>

```

In here, when we change the code in `index.html`, the page in browser will auto refresh.

**But** when we remove the `script` in `index.html`, after starting the webpack dev server, it won't reload the page when we change the code in `index.html`, if want to see the change, we have to manually refresh the browser. See the code below:

index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>mini-react</title>
    <!-- <script src="index.bundle.js"></script> -->
  </head>
  <body>
    <div id="root">asaaasssssaaf</div>
  </body>
</html>

```

### Answer

## What's the difference beteween live reload and hot reload?
