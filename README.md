# Polymer Webpack Demo with npm elements

## Setup

```
npm i
bower i
npm start
```
Changes in comparison to [polymer-starter-kit demo](https://github.com/webpack-contrib/polymer-webpack-loader/tree/master/demo)

1. Added ignoreLinksFromPartialMatches option to the loader to ensure that any relative path links to polymer.html inside of an npm element would be ignored since my-element.html is linking to the bower_components version of polymer.html.

```
module: {
    rules: [
      {
        // If you see a file that ends in .html, send it to these loaders.
        test: /\.html$/,
        // This is an example of chained loaders in Webpack.
        // Chained loaders run last to first. So it will run
        // polymer-webpack-loader, and hand the output to
        // babel-loader. This let's us transpile JS in our `<script>` elements.
        use: [
          { loader: 'babel-loader', 
            options: {
              plugins: ['syntax-dynamic-import']
            }
          },
          { loader: 'polymer-webpack-loader',
            options: {
              // We need to ignore any relative path reference to polymer.html because
              // we only want to use the version in bower_components. 
              ignoreLinksFromPartialMatches: ['./polymer/polymer.html']
            }
          },
        ]
      },
      {
        // If you see a file that ends in .js, just send it to the babel-loader.
        test: /\.js$/,
        use: {
          loader: 'babel-loader'
        },
        // This line tells Webpack not to transpile .js files coming out of
        // node_modules.
        exclude: /node_modules/
      }
    ]
  },
```
2. Changed the link in the my-elements.html to use polymer instead of polymer-element.
```
<link rel="import" href="../bower_components/polymer/polymer.html">
```
instead of 
```
<link rel="import" href="../bower_components/polymer/polymer-element.html">
```
