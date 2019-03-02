# react-webpack-babel-eslint
React configured to use with Webpack, Babel and ESLint

## Instruction how to create it on your own manually
1. Create a `package.json` file:
  ```
  npm init
  ```
  Or if you want to skip all the questions, add the `-y` flag:
  ```
  npm init -y
  ```
2. We need to install all the dependencies:
  ```
  npm i react react-dom webpack webpack-cli webpack-dev-server @babel/core babel-loader @babel/preset-env @babel/preset-react eslint eslint-loader babel-eslint html-webpack-plugin html-loader -D
  ```

	Explanation:
	* `react` - React library
	* `react-dom` - ReactDOM library to render React
	* `webpack` - module bundler
	* `webpack-cli` - to use webpack in the command line
	* `webpack-dev-server` - development server
	* `@babel/core` - transforms  ES6 code into ES5
	* `babel-loader` - Babel loader for webpack
	* `@babel/preset-env` - for compiling Javascript ES6 code down to ES5
	* `@babel/preset-react` - for compiling JSX and other stuff down to Javascript
	* `html-webpack-plugin` -  generates an HTML file with `<script>` injected, writes this to `dist/index.html`, and minifies the file
	* `html-loader` - for exporting HTML
	* `eslint` - ESLint JavaScript linter
	* `eslint-loader` - ESLint loader for webpack
	* `babel-eslint` - wrapper for Babel's parser used for ESLint
3. Create a file `.gitignore`:
	```
	node_modules/
	dist/
	```
4. Add the following scripts to `package.json`:
	```
	"scripts": {
	    "start": "webpack-dev-server --mode development --open",
	    "build": "webpack --mode production"
	  },
	```
5. Create a file `webpack.config.js` with Webpack config:
	```
	const HtmlWebPackPlugin = require("html-webpack-plugin");
	module.exports = {
	  module: {
	    rules: [
	      {
	        test: /\.(js|jsx)$/,
	        exclude: /node_modules/,
	        use: ['babel-loader', 'eslint-loader']
	      },
	      {
	        test: /\.html$/,
	        use: [
	          {
	            loader: "html-loader"
	          }
	        ]
	      }
	    ]
	  },
	  plugins: [
	    new HtmlWebPackPlugin({
	      template: "./src/index.html",
	      filename: "./index.html"
	    })
	  ]
	};
	```
6. Create a file `.babelrc` with Babel config:
	```
	{
	  "presets": [
	    "@babel/preset-env",
	    "@babel/preset-react"
	  ]
	}
	```
7. Create a file `.eslintrc.js` with ESLint config:
	```
	module.exports = {
	  parser: "babel-eslint",
	};
	```
8. Create a file `src/App.js` with sample component content:
	```
	import React, { Component } from 'react';

	class App extends Component {
	  render() {
	    return (
	      <div className="App">
	        Basic App demo
	      </div>
	    );
	  }
	}

	export default App;
	```
9. Create a file `src/index.js` and place the following code to render a component:
	```
	import React from "react";
	import ReactDOM from "react-dom";
	import App from './App';

	ReactDOM.render(<App />, document.getElementById('root'));
	```
10. Create a file `src/index.html` to render website:
	```
	<!DOCTYPE html>
	<html lang="en">
	<head>
	  <meta charset="utf-8">
	  <meta name="viewport" content="width=device-width, initial-scale=1.0">
	  <title>React App</title>
	</head>
	<body>
	  <noscript>You need to enable JavaScript to run this app.</noscript>
	  <div id="root"></div>
	</body>
	</html>
	```
11. To start development of project use command:
	```
	npm start
	```
12. To create bundle (in `dist/` folder) that you can put on the server use command:
	```
	npm run build
	```

## Author
Copyright (c) 2019 [Piotr Kołodziejczyk](https://github.com/frontend-london)

## License
This project is licensed under the MIT License - see the LICENSE.md file for details

