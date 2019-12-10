# config webpack load multiple file 
```js
const fs = require('fs');
const path = require('path');
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

const input = []
fs.readdirSync(path.resolve(__filename, '../src/styles/effects/')).forEach(filename => input.push(filename));

const config = {
  mode: 'development',
  // entry: './src/styles/effects/xo-e-slide-right.scss',
  // output: {
  //   path: path.resolve(__dirname, 'dist'),
  //   filename: 'main.css'
  // },
  devServer: {
    contentBase: './dist',
  },
  module: {
    rules: [
      {
        test: /\.(s*)css$/,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          'sass-loader',
        ]
      },
    ],
  }
}


const listObject = input.map(e => Object.assign({}, config, {
  entry: './src/styles/effects/' + e,
  // output: {
  //   path: path.join(__dirname, "dist"),
  //   filename: e.replace('.scss', '.css')
  // },
  plugins: [new MiniCssExtractPlugin({
    filename: e.replace('.scss', '.css')
  }), require("autoprefixer")]
}))



module.exports = listObject
// module.exports = config
```