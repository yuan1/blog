---
title: How To Enable ES6 Imports in Node.JS
tags: [ES6,NODEJS,JS]
categories:
  - Html
toc: false
date: 2019-08-12 14:30:09
---


package.json
```javascript
"devDependencies": {
    "@babel/core": "^7.5.5",
    "@babel/preset-env": "^7.5.5",
    "@babel/register": "^7.5.5"
}

```

.babelrc
```javascript
{
  "presets": ["@babel/preset-env"]
}

```


entry point node.js app
```javascript
require("@babel/register")({})
    
// Import the rest of our application.
module.exports = require('./index.js')

```

Link How To Enable ES6 Imports in Node.JS  https://timonweb.com/posts/how-to-enable-es6-imports-in-nodejs/
