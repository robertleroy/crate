# Webpack Primer 
---
# **Setup**

## Init
```
npm init -y

npm i webpack webpack-cli webpack-dev-server --save-dev
```

## Edit package.json
```
"scripts": {
  "dev": "webpack --mode development"
},
```

## `./src` Folder / Entry File
```
mkdir src
echo 'console.log("Hello webpack!")' > src/index.js
```

## Run Webpack (-creates `./dist` [webpack bundle])
```
npm run dev
```

## Create Config File
```
touch webpack.config.js
```

## [optional...] Change entry point or dist path... 
``` js
/* webpack.config.js */

// example //
const path = require("path");

module.exports = {
  entry: { 
    index: path.resolve(__dirname, "source", "index.js") 
  },

  output: {
    path: path.resolve(__dirname, "build")
  }
};
```

- Now webpack will look in source/index.js for the first file to load. 
- Now webpack will put the bundle in build instead of dist. 
- (To keep things simple we'll stick to the default in this guide).


---

# **HTML Plugin**
- loads our HTML files
- injects the bundle(s) in the same file

```
npm i html-webpack-plugin --save-dev
```

## Configure
``` js
/* webpack.config.js */

const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require("path");

module.exports = {
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, "src", "index.html")
    })
  ]
};

```

## Create a simple HTML file in src/index.html
``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Webpack tutorial</title>
</head>
<body>

</body>
</html>
```

## Webpack Dev Server
``` 
npm i webpack-dev-server --save-dev 
```
``` js
// package.json

"scripts": {
  "dev": "webpack --mode development",
  "start": "webpack-dev-server --mode development --open",
},

```

## Run Server
```
npm start
```
---

# **Loaders**


## Css & Style loader
```
npm i css-loader style-loader --save-dev
```

##
``` js
/* webpack.config.js */

//
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  //
};
```

## Order Matters:
- Here "style-loader" appears before "css-loader".

## SASS
``` js
// the same loaders + sass & sass-loader
npm i css-loader style-loader sass-loader sass --save-dev
```


##
``` js
/* webpack.config.js */

const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require("path");

module.exports = {
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ["style-loader", "css-loader", "sass-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, "src", "index.html")
    })
  ]
};
```

## MiniCssExtractPlugin
```

```

---

# Javascript / Babel

Compiles code and modules to backwards compatible format.
- babel core, the actual engine
- babel preset env for compiling modern Javascript down to ES5
- babel loader for webpack

webpack works fine without babel.  
The transpiling process is only necessary for shipping ES5

```
npm i @babel/core babel-loader @babel/preset-env --save-dev
```

## Babel Config Json
``` json
/* babel.config.json */

{
  "presets": [
    "@babel/preset-env"
  ]
}

```

## 
``` js
/* webpack.config.js - after sass - */

  {
    test: /\.js$/,
    exclude: /node_modules/,
    use: ["babel-loader"]
  }
```
---
# ES Modules

## Create a module
``` js
/* src/common/usersAPI.js */

const ENDPOINT = "https://jsonplaceholder.typicode.com/users/";

export function getUsers() {
  return fetch(ENDPOINT)
    .then(response => {
      if (!response.ok) throw Error(response.statusText);
      return response.json();
    })
    .then(json => json);
}
```

## Load Module in index.js
``` js
/* src/index.js */

import { getUsers } from "./common/usersAPI";
import "./style.scss";
console.log("Hello webpack!");

getUsers().then(json => console.log(json));
```

---
# Production mode
Production Mode Optimizations:
- minification to reduce the bundle size
- scope hoisting
- set process.env.NODE_ENV to "production"

To configure webpack in production mode:

``` js
/* package.json */

"scripts": {
  "dev": "webpack --mode development",
  "start": "webpack-dev-server --mode development --open",
  "build": "webpack --mode production"
},
```
Now running `npm run build` produces a minified bundle.

---
# Code Splitting
Optimization to:
- avoid big bundles
- avoid dependencies duplication
- keep initial bundle (entry point) under 200KB

3 Strategies
- multiple entry points
- optimization.splitChunks
- dynamic imports

<br>

1. ### **multiple entry points**
  - works well for smaller projects
  - not scalable in the long run    

<br>

2. ### **optimization.splitChunks**
- splits modules from main entry point
- leaves entry point small

``` js
/* webpack.config.js */

// ... modules ... //
},
optimization: {
  splitChunks: { chunks: "all" }
},
// ... plugins ... //
```

<br>

3. ### Dynamic Imports**
- Lazy load modules as needed
  - respond to a click or route change
- *~ reco mended ~*

## `example:`
``` js
const getUserModule = () => import("./common/usersAPI");

const btn = document.getElementById("btn");

btn.addEventListener("click", () => {
  getUserModule().then(({ getUsers }) => {
    getUsers().then(json => console.log(json));
  });
});

```
This function does not loads the module until the click event.  
This function also generates a generic name for the `dist` file, like `/dist/0.js`.  
Alias a `webpackChunkName` to create a meaningful name:

``` js
const getUserModule = () =>
  import(/* webpackChunkName: "usersAPI" */ "./common/usersAPI");

/* creates ./dist/usersAPI.js */
```

one more example 
``` js
const btn = document.getElementById("btn");

btn.addEventListener("click", () => {
  // loads named export
  import( /* webpackChunkName: "funcA" */ "./util.js")
    .then(({ funcA }) => {
      funcA();
    });
});
```

---
# Resources:
  - [Webpack](https://webpack.js.org/)
  - [This tutorial](https://www.valentinog.com/blog/webpack/)
  - [All I need to know about ECMAScript modules](https://www.valentinog.com/blog/es-modules/)
  - [Survive JS - webpack](https://survivejs.com/webpack/)
