---
layout: docs
title: Parcel
description: Learn how to include Bootstrap in your project using Parcel.
group: getting-started
toc: true
---

## Installing Bootstrap

[Install bootstrap]({{< docsref "/getting-started/download#npm" >}}) as a Node.js module using npm.

Bootstrap depends on [Popper](https://popper.js.org/), which is specified in the `peerDependencies` property.
This means that you will have to make sure to add both of them to your `package.json` using `npm install popper.js`.

## Importing JavaScript

Import [Bootstrap's JavaScript]({{< docsref "/getting-started/javascript" >}}) by adding this line to your app's entry point (usually `src/index.js`):

{{< highlight js >}}
// Import all plugins
import * as bootstrap from 'bootstrap';
//Or import only needed plugins
import { Tooltip as Tooltip, Toast as Toast, Popover as Popover } from 'bootstrap';
{{< /highlight >}}

Alternatively, if you only need just a few of our plugins, you may **import plugins individually** as needed:

{{< highlight js >}}
import Alert as Alert from '../node_modules/bootstrap/js/dist/alert';
...
{{< /highlight >}}

## Importing Styles

### Importing Precompiled Sass

To enjoy the full potential of Bootstrap and customize it to your needs, use the source files as a part of your project's bundling process.

First, create your own `scss/custom.scss` and use it to override the [built-in custom variables]({{< docsref "/customize/sass" >}}). Then, use it to add your customized variables, followed by Bootstrap import:

{{< highlight scss >}}
//override buit-in custom variables
//** Background color for `<body>`.
$body-bg: #9cf;

// breadcrumb
$breadcrumb-divider: quote(">");

// import bootstrap scss
import '../../scss/custom.scss'; // Import our scss file
{{< /highlight >}}

For Bootstrap to compile, make sure you install and use the required loaders: [sass-loader](https://github.com/webpack-contrib/sass-loader), [postcss-loader](https://github.com/postcss/postcss-loader) with [Autoprefixer](https://github.com/postcss/autoprefixer#webpack). With minimal setup, your webpack config should include this rule or similar:

{{< highlight js >}}
...
{
  test: /\.(scss)$/,
  use: [{
    loader: 'style-loader', // inject CSS to page
  }, {
    loader: 'css-loader', // translates CSS into CommonJS modules
  }, {
    loader: 'postcss-loader', // Run postcss actions
    options: {
      plugins: function () { // postcss plugins, can be exported to postcss.config.js
        return [
          require('autoprefixer')
        ];
      }
    }
  }, {
    loader: 'sass-loader' // compiles Sass to CSS
  }]
},
...
{{< /highlight >}}

### Importing Compiled CSS

Alternatively, you may use Bootstrap's ready-to-use CSS by simply adding this line to your project's entry point:

{{< highlight js >}}
import 'bootstrap/dist/css/bootstrap.min.css';
{{< /highlight >}}

In this case you may use your existing rule for `css` without any special modifications to webpack config, except you don't need `sass-loader` just [style-loader](https://github.com/webpack-contrib/style-loader) and [css-loader](https://github.com/webpack-contrib/css-loader).

{{< highlight js >}}
...
module: {
  rules: [
    {
      test: /\.css$/,
      use: ['style-loader', 'css-loader']
    }
  ]
}
...
{{< /highlight >}}
