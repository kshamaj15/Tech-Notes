At its core, webpack is a static module bundler for modern JavaScript applications.

To get started you only need to understand its Core Concepts:
### Entry
An entry point indicates which module webpack should use to begin building out its internal dependency graph. Webpack will figure out which other modules and libraries that entry point depends on (directly and indirectly).
By default its value is ./src/index.js, but you can specify a different (or multiple entry points) by setting an entry property in the webpack configuration. For example:
webpack.config.js
```
module.exports = {
  entry: './path/to/my/entry/file.js',
};
```
```
module.exports = {
  entry: {
    home: './home.js',
    about: './about.js',
    contact: './contact.js',
  },
};
```
### Output
The output property tells webpack where to emit the bundles it creates and how to name these files. It defaults to ./dist/main.js for the main output file and to the ./dist folder for any other generated file.

You can configure this part of the process by specifying an output field in your configuration:

webpack.config.js
```
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js',
  },
};
```
### [Loaders](https://webpack.js.org/concepts/loaders/)
Out of the box, webpack only understands JavaScript and JSON files. Loaders allow webpack to process other types of files and convert them into valid modules that can be consumed by your application and added to the dependency graph.

At a high level, loaders have two properties in your webpack configuration:

- The `test` property identifies which file or files should be transformed.
- The `use` property indicates which loader should be used to do the transforming.
webpack.config.js
```
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js',
  },
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
};
```
"Hey webpack compiler, when you come across a path that resolves to a '.txt' file inside of a require()/import statement, use the raw-loader to transform it before you add it to the bundle."

### [Plugins](https://webpack.js.org/api/plugins/)
While loaders are used to transform certain types of modules, plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables.

Tip
### Mode
By setting the mode parameter to either development, production or none, you can enable webpack's built-in optimizations that correspond to each environment. The default value is production.
Browser Compatibility
```
module.exports = {
  mode: 'production',
};
```

### Dependency Graph
Any time one file depends on another, webpack treats this as a dependency.

