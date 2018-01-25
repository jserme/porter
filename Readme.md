[![NPM Downloads](https://img.shields.io/npm/dm/porter.svg?style=flat)](https://www.npmjs.com/package/porter)
[![NPM Version](http://img.shields.io/npm/v/porter.svg?style=flat)](https://www.npmjs.com/package/porter)
[![Build Status](https://travis-ci.org/erzu/porter.svg)](https://travis-ci.org/erzu/porter)

Porter is a consolidated browser modules framework featuring module transformation on the fly.

## How to

You need a main entry point for your app's JS and/or CSS.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>An Porter Example</title>
  <!-- CSS ENTRY -->
  <link rel="stylesheet" type="text/css" href="/app.css">
</head>
<body>
  <h1>An Porter Example</h1>
  <!-- JAVASCRIPT ENTRY -->
  <script src="/app.js?main"></script>
</body>
</html>
```

In js files, you can use CMD `require` dependencies:

```js
const $ = require('jquery')
const cropper = require('cropper')
```

Or esModule:

```js
 * as React from 'react'
```

And in stylesheets, you can `@import` dependencies too:

```css
@import 'cropper/dist/cropper.css';   /* stylesheets in node_modules */
@import './nav.css';                  /* stylesheets in components */
```

To achieve this, just setup the middleware provided by porter. For Koa:

```js
const Koa = require('koa')
const porter = require('@cara/porter')
const app = new Koa()

// The paths of JS/CSS components
app.use(porter({ paths: 'components' }))
```

For older versions of Koa that require generator functions:

```js
const koa = require('koa')
const porter = require('@cara/porter')
const app = koa()

app.use(porter({ type: 'GeneratorFunction' }))
```

For Express:

```js
const express = require('express')
const porter = require('@cara/porter')
const app = express()

// that's it
app.use(porter({ type: 'Function' }))
```

When it's time to be production ready, simply run:

```js
const porter = require('@cara/porter')

Promise.all[
  porter.compileAll({ match: 'app.js' }),           // js components and modules
  porter.compileStyleSheets({ match: 'app.css' })   // css files
])
  .catch(function(err) {
    console.error(err.stack)
  })
```
