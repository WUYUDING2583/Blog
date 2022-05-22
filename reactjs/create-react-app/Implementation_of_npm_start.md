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