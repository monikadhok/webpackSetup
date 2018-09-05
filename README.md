# Setting up the Project

First you'll need [Node.js](https://nodejs.org) and the package manager
that comes with it: [npm](https://www.npmjs.com/).

Once you've got that working, head to the command line where we'll set
up our project.

## Clone the Tutorial

```
git clone https://github.com/reactjs/react-router-tutorial
cd react-router-tutorial
cd lessons/01-setting-up
npm install
npm start
```

Now open up [http://localhost:8080](http://localhost:8080)

Feel free to poke around the code to see how we're using webpack and npm
scripts to run the app.

You should see a "Hello React Router" message in the browser.

## Make Some Changes

Open up `modules/App.js` and change the text to something like "Hello
<your name>". The browser automatically reloads with your new code.

---

[Next: Rendering a Router](../02-rendering-a-route/)

Webpack:

1) Installation:
npm install webpack --save-dev

Once it is installed, add following to package.json
//...
    "scripts": {
        "build": "webpack -p",
        "watch": "webpack --watch"
    },
//...

-p : stands for production 
watch : automatically bundles our files when there is a change in files.


2) webpack.config.js

var path = require('path');

module.exports = {
  entry: './assets/js/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};

entry : tells the webpack which is our main javaScript file. 
output : name and path of our bundle 

3) Webpack modules 

webpack modules can express their dependencies in a variety of ways. A few examples are:

An ES2015 import statement
A CommonJS require() statement
An AMD define and require statement
An @import statement inside of a css/sass/less file.
An image url in a stylesheet (url(...)) or html (<img src=...>)file.

greeter.js
function greet() {
    console.log('Have a great day!');
};

export default greet;

index.js
import greet from './greeter.js';

console.log("I'm the entry point");
greet();


4) Requiring libraries

First we need to install the library via npm:

npm install moment --save
Then in our greeting module, we simply import the library exactly the same way we imported local modules in the previous point:

greeter.js
import moment from 'moment';

function greet() {
    var day = moment().format('dddd');
    console.log('Have a great ' + day + '!');
};

export default greet;


5) Loaders

Loaders are the webpack's way to execute tasks during bundling 
and pre/post process the files in some manner. For example, 
linting JSHintLoader is one of the popular loaders 

npm install jshint jshint-loader --save-dev

Afterwords, we are going to add a few lines to our webpack config file. This will initialize the loader, tell it what type of files to check, and which files to ignore.

webpack.config.js
var path = require('path');

module.exports = {
  entry: './assets/js/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  // Add the JSHint loader
  module: {
    rules: [{
      test: /\.js$/, // Run the loader on all .js files
      exclude: /node_modules/, // ignore all files in the node_modules folder
      use: 'jshint-loader'
    }]
  }
};




