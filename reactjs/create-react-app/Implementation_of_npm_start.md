# 1. Overview

In this chapter, we will go through the implementation detail of `npm start` of `create-react-app`.

> React Version: v18.1.0 

The overview steps of `npm start` are below:

1. Check required files.
2. Check browsers.
3. Choose port.
4. Start webpack dev server.
5. Open browser.

![Overview](./assets/Implementation_of_npm_start/Overview.png)

# 2. Check required files

The files we need as basic are listed below and all of them are in root folder:

1. `public/index.html`
2. `src/index.js`

# 3. Check browsers

## 3.1 Overview

![CheckBrowsers](./assets/Implementation_of_npm_start/CheckBrowsers.png)

## 3.2  Load browserslist config

Load the `browserslist` config user have set in the project.

```js
browserslist.loadConfig()
```

If the `browserslist` configuration exists, we can resolve this and finish checking browsers. Otherwise need to check this checking behaviour is a second time checking.

## 3.3 Set browsers

If user don't set `browserlist` in project, then we should ask user if set the default `browserlist` in the project.

```js
 const question = {
    type: 'confirm',
    name: 'shouldSetBrowsers',
    message:
      chalk.yellow("We're unable to detect target browsers.") +
      `\n\nWould you like to add the defaults to your ${chalk.bold(
        'package.json'
      )}?`,
    initial: true,
  };

  return prompts(question).then(answer => answer.shouldSetBrowsers);
```

If user allow to set default browsers, then we can write it into the project `package.json`