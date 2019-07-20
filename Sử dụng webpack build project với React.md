# 1. Setting Up Webpack + Babel

## **A. Initialize Repository:**

If you haven’t already, initialize your project through the terminal with NPM. This will create a package.json where our dev dependencies will be added. If you have already done this, you can skip this Part A.

```
npm init
```

## **B.** NPM **Dev Dependencies:** Setting Up:

Here are all of necessary and latest versions of the Webpack and Babel dependencies to get everything working as of mid 2018. To see why and what each dependency does, check out Part C.

**Note:** We will be using Babel 7, which is why there is an “@” symbol as a prefix for the babel dependencies. `@babel/` distinguishes these dependencies as [**Scoped Packages**](https://babeljs.io/docs/en/v7-migration), which means the package prefix is the account. Previously, anyone could just name a package `babel-hacker-package`, which someone would think Babel created the package. In Babel 7 Scoped Package, there is an uniform naming convention and there will be no more issues with accidental or intentional name stealing.

**Note:** If you’re using Node.js version 5 or higher, you don’t need to include — save since it is now automatically saved to your dependencies. To identify the version of Node.js you’re running, type node -v in the terminal.

## **Webpack:**

```
npm install webpack webpack-cli webpack-dev-server --save-dev
```

## **Babel:**

```
npm install @babel/cli @babel/core @babel/node @babel/preset-env @babel/preset-react @babel/register --save-dev
```

## **JS/JSX & CSS Loaders:**

```
npm install babel-loader style-loader css-loader
```

## C. Each Dev Dependency Explained:

I’ve done quite a bit of research on the available dependencies for Webpack and Babel. Below is a brief explanation of what they do.

## Webpack:

- **webpack** (Webpack Compiler/Bundler) ([NPM Link](https://www.npmjs.com/package/webpack))
- **webpack-cli** (Command Line Interface that communicates to the Webpack Compiler/Bundler) ([NPM Link](https://www.npmjs.com/package/webpack-cli))
- **webpack-dev-server** (Dùng trong development, cấu hình trong ```package.json``` để trình duyệt tự refesh nếu có thay đổi) ([NPM Link](https://www.npmjs.com/package/webpack-dev-server))

## **Babel:**

- **@babel/core** (Chuyển đổi mã ES6 sang ES5) ([NPM Link](https://www.npmjs.com/package/babel-core))

- **@babel/cli** (Command Line Interface that communicates to the Babel Transpiler) ([NPM Link](https://www.npmjs.com/package/babel-cli))

- **@babel/register** (Transpiles files required by Node.js with the extensions .es6, .es, .jsx and .js) ([NPM Link](https://www.npmjs.com/package/babel-register))

- **@babel/preset-env** (Transpiles files using ES6, ES7, and ES8. The same as babel-preset-latest, which includes babel-preset-es2015, babel-preset-es2016, and babel-preset-es2017. However, babel-preset-latest is deprecated and replaced by babel-preset-env, so that’s why we’re using babel-preset-env. It’s the package of all packages) ([NPM Link](https://www.npmjs.com/package/babel-preset-env))

  > Preset giúp babel chuyển đổi mã ES6, ES7 và ES8 sang ES5.

- **@babel/preset-react** (Transpiles files using React. This is necessary if your project is using React) ([NPM Link](https://www.npmjs.com/package/babel-preset-react))

  > Preset giúp chuyển đổi mã JSX sang javascript

## Loaders:

- **babel-loader** (Loads the files to Webpack for Babel to transpile) ([NPM Link](https://www.npmjs.com/package/babel-loader))
- **style-loader** (Add exports of a module as style to DOM. Necessary when using css-loader, sass-loader, or less-loader) ([NPM Link](https://www.npmjs.com/package/style-loader))
- **css-loader** (Loads CSS file with resolved imports and returns CSS code) ([NPM Link](https://www.npmjs.com/package/css-loader))

# 2. Setting Up Babel (.babelrc)

In the root of your project folder, create a `.babelrc` file.

## A. Create Basic Babel File Structure:

```
{  "presets": []}
```

## **B. Add Babel Presets:**

Let’s now add those dependencies were installed earlier:

- **@babel/preset-env** (ES6, ES7, and ES8 files)
- **@babel/preset-react** (React Files)

```js
{  "presets": [    "@babel/preset-env",    "@babel/preset-react"  ]}
```

The Babel file is configured and complete. Now let’s move onto the Webpack configuration file.

# 3. Setting Up Webpack (webpack.config.js)

In the root of your project folder, the same place where your .babelrc should be located, create a webpack.config.js file. Compared to the Babel config file, this file is different and we need to require the following packages we installed. Note: path is part of Node.js, so you won’t have to install any additional packages if you have Node.js installed.

## A. What Each Dev Dependency Does:

- **path** (Included in Node.js. Creates a dynamic input/output path from a root directory) ([Documentation](https://nodejs.org/docs/latest/api/path.html))
- **html-webpack-plugin** (Auto generates an html file from your template index.html to serve up your application) ([NPM Link](https://www.npmjs.com/package/html-webpack-plugin))
- **babel-register** (Allows ES6+ to be used on Node.js files) ([NPM Link](https://www.npmjs.com/package/babel-register))

## B. The Basic Webpack File Structure:

**Note:** We will be adding to this file structure from B to F, so if you want the completed Webpack file, scroll down to “F. Options + Webpack Development Tools.”

```javascript
// Imports: Dependencies
const path = require('path');
require("babel-register");
// Webpack Configuration
const config = {
  
  
// Entry
  
entry: {'PATH TO YOUR INDEX.JSX FILE'},
  // Output
  
output: {
    path: path.resolve(__dirname, '
PATH TO SEND BUNDLED/TRANSPILED CODE'),
    filename: 'bundle.js',
  },
  // Loaders
  
module: {
    rules : [
      // JavaScript/JSX Files
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: ['babel-loader'],
      },
      // CSS Files
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      }
    ]
  },
  // Plugins
  
plugins: [],
};
// Exports
module.exports = config;
```

## **C. Entry:**

Entry is the first file you want Webpack to start with. For React applications, we want to start at the index.js file. With my file structure, the entry point would look like this:

```js
entry: {'./client/src/index.jsx'}
```

## **D. Output:**

Output is where the files transpiled by Babel and compiled from Webpack will be sent, so we will output our file as bundle.js to the “dist” or distribution folder.

```js
path: path.resolve(__dirname, './client/dist'),  filename: 'bundle.js'
```

## E. Loaders:

Loaders are how your static assets are loaded into Webpack. If you are using .js files instead of .jsx files, you can correct the configuration by replacing /\.jsx$/ with /\.js$/ on “test” as shown below.

```js
{  test: /\.js$/,  exclude: /node_modules/,  use: ['babel-loader']}
```

If you are using .sass files instead of .css files, you can correct the configuration by replacing /\.css$/ with /\.sass$/ on the field “test” as shown below. You will have to install additional dev dependencies, depending on the your file types.

```js
{  test: /\.sass$/,  use: ['style-loader', 'sass-loader']}
```

## **F. Plugins:**

What html-webpack-plugin does is it generates an index.html file for you if there isn’t one. Here’s an example of how the file structure would now look with a plugin file (The changes are in bold):

- **html-webpack-plugin** (Plugin auto generates HTML files to serve your bundles) ([NPM Link](https://www.npmjs.com/package/html-webpack-plugin))

```js
// Imports
const path = require('path');
const htmlWebpackPlugin = require('html-webpack-plugin')
require("babel-register");
// Webpack Configuration
const config = {
  // Entry
  
entry: {'./client/src/index.js'},
  
  
// Output
  
output: {
    path: path.resolve(__dirname, './client/dist'),
    filename: 'bundle.js',
  },
  // Loaders
  
module: {
    rules : [
      
// JavaScript/JSX Files
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: ['babel-loader'],
      },
      
// CSS Files
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      }
    ]
  },
  // Plugins
  
plugins: [
    new htmlWebpackPlugin({
      template: './client/dist/index.html',
      filename: 'index.html',
      hash: true
    })
  ],
};
// Exports
module.exports = config;
```

- **template:** Refers to the path where you want the file to be generated
- **filename:** Refers to what you want the file to be called, in which index.html is standard
- **hash:** A true or false value that hashes the source url for your application

## **F. Options +** Webpack Development Tools:

Below, we are going to add the `watch` [Webpack Option](https://webpack.js.org/configuration/#options) and the `source-map`[Webpack Devtool](https://webpack.js.org/configuration/devtool/) to our Webpack configuration file.

- **watch** (Webpack will continue to watch for changes in any of the resolved files)
- **source-map** (Has there has ever been a time debugging and the line in the error isn’t the line in your code? Source Map will provide detailed debugging by adding meta info for the browser’s console)

```js
// Imports
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin')

require("babel-register");
// Webpack Configuration
const config = {
  // Entry
  
entry: {'./client/src/index.js'},
  
  
// Output
  
output: {
    path: path.resolve(__dirname, './client/dist'),
    filename: 'bundle.js'
  },
  // Loaders
  
module: {
    rules : [
      
// JavaScript/JSX Files
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: ['babel-loader']
      },
      
// CSS Files
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      }
    ]
  },
  // Plugins
  
plugins: [
    new HtmlWebpackPlugin({
      template: './client/dist/index.html',
      filename: 'index.html',
      hash: true
    })
  ]
  // OPTIONAL
  // Reload On File Change
  // Có thể bỏ cái này và xử lý ở package.json
  watch: true,
  // Development Tools (Map Errors To Source File)
  devtool 'source-map',
};
// Exports
module.exports = config;
```

# You’re All Done, You Webpack & Babel Prodigy.

# Cài đặt build webpack bằng NPM

```
"start": "webpack --mode development --watch",
"build": "webpack --mode production"
```

> Nếu đã cài đặt ```webpack-dev-server```
>
> ```"start": "webpack-dev-server --mode development --open --hot"```
>
> Thêm `--open` và `--hot` để mở và làm mới trang web bất cứ khi nào có bất kỳ thay đổi nào được thực hiện đối với các `components`. 

# Change port 

Nếu sử dụng ```webpack-dev-server```, đổi port ta thêm đoạn sau trong ```webpack.config.js```

```js
devServer: {
    port: 3000
}
```

---

Xem thêm

[create-react-wp](https://github.com/dungnt11/create-react-wp.git)

# Lazy load & fix URL cannot GET when reload

[Lazy load](https://reacttraining.com/react-router/web/guides/code-splitting) 

Fix cannot get url [fix](https://reacttraining.com/react-router/web/guides/code-splitting)

```javascript
var path = require('path');
var HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './app/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'index_bundle.js',
    publicPath: '/'
  },
  module: {
    rules: [
      { test: /\.(js)$/, use: 'babel-loader' },
      { test: /\.css$/, use: [ 'style-loader', 'css-loader' ]}
    ]
  },
  devServer: {
    historyApiFallback: true,
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: 'app/index.html'
    })
  ]
};

```

