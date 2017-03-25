# api documentation for  [dotenv (v4.0.0)](https://github.com/motdotla/dotenv#readme)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-dotenv.svg)](https://travis-ci.org/npmdoc/node-npmdoc-dotenv)
#### Loads environment variables from .env file

[![NPM](https://nodei.co/npm/dotenv.png?downloads=true)](https://www.npmjs.com/package/dotenv)

[![apidoc](https://npmdoc.github.io/node-npmdoc-dotenv/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-dotenv_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-dotenv/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-dotenv/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "scottmotte"
    },
    "bugs": {
        "url": "https://github.com/motdotla/dotenv/issues"
    },
    "dependencies": {},
    "description": "Loads environment variables from .env file",
    "devDependencies": {
        "babel": "5.8.23",
        "coveralls": "^2.11.9",
        "lab": "11.1.0",
        "semver": "5.3.0",
        "should": "11.1.1",
        "sinon": "1.17.6",
        "standard": "8.4.0",
        "standard-markdown": "2.2.0"
    },
    "directories": {},
    "dist": {
        "shasum": "864ef1379aced55ce6f95debecdce179f7a0cd1d",
        "tarball": "https://registry.npmjs.org/dotenv/-/dotenv-4.0.0.tgz"
    },
    "engines": {
        "node": ">=4.6.0"
    },
    "gitHead": "fdd0923e82e12a6e29b65898990201857141e75d",
    "homepage": "https://github.com/motdotla/dotenv#readme",
    "keywords": [
        "dotenv",
        "env",
        ".env",
        "environment",
        "variables",
        "config",
        "settings"
    ],
    "license": "BSD-2-Clause",
    "main": "lib/main.js",
    "maintainers": [
        {
            "name": "jcblw",
            "email": "jacoblowe2.0@gmail.com"
        },
        {
            "name": "maxbeatty",
            "email": "max@beatty.me"
        },
        {
            "name": "motdotla",
            "email": "mot@mot.la"
        },
        {
            "name": "scottmotte",
            "email": "scott@scottmotte.com"
        }
    ],
    "name": "dotenv",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/motdotla/dotenv.git"
    },
    "scripts": {
        "lint": "standard",
        "lint-md": "standard-markdown",
        "postlint": "npm run lint-md",
        "pretest": "npm run lint",
        "test": "lab test/* -r lcov | coveralls"
    },
    "version": "4.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module dotenv](#apidoc.module.dotenv)
1.  [function <span class="apidocSignatureSpan">dotenv.</span>config (options)](#apidoc.element.dotenv.config)
1.  [function <span class="apidocSignatureSpan">dotenv.</span>load (options)](#apidoc.element.dotenv.load)
1.  [function <span class="apidocSignatureSpan">dotenv.</span>parse (src)](#apidoc.element.dotenv.parse)



# <a name="apidoc.module.dotenv"></a>[module dotenv](#apidoc.module.dotenv)

#### <a name="apidoc.element.dotenv.config"></a>[function <span class="apidocSignatureSpan">dotenv.</span>config (options)](#apidoc.element.dotenv.config)
- description and source-code
```javascript
function config(options) {
  var path = '.env'
  var encoding = 'utf8'

  if (options) {
    if (options.path) {
      path = options.path
    }
    if (options.encoding) {
      encoding = options.encoding
    }
  }

  try {
    // specifying an encoding returns a string instead of a buffer
    var parsedObj = parse(fs.readFileSync(path, { encoding: encoding }))

    Object.keys(parsedObj).forEach(function (key) {
      process.env[key] = process.env[key] || parsedObj[key]
    })

    return { parsed: parsedObj }
  } catch (e) {
    return { error: e }
  }
}
```
- example usage
```shell
...
'''

## Usage

As early as possible in your application, require and configure dotenv.

'''javascript
require('dotenv').config()
'''

Create a '.env' file in the root directory of your project. Add
environment-specific variables on new lines in the form of 'NAME=VALUE'.
For example:

'''
...
```

#### <a name="apidoc.element.dotenv.load"></a>[function <span class="apidocSignatureSpan">dotenv.</span>load (options)](#apidoc.element.dotenv.load)
- description and source-code
```javascript
function config(options) {
  var path = '.env'
  var encoding = 'utf8'

  if (options) {
    if (options.path) {
      path = options.path
    }
    if (options.encoding) {
      encoding = options.encoding
    }
  }

  try {
    // specifying an encoding returns a string instead of a buffer
    var parsedObj = parse(fs.readFileSync(path, { encoding: encoding }))

    Object.keys(parsedObj).forEach(function (key) {
      process.env[key] = process.env[key] || parsedObj[key]
    })

    return { parsed: parsedObj }
  } catch (e) {
    return { error: e }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.dotenv.parse"></a>[function <span class="apidocSignatureSpan">dotenv.</span>parse (src)](#apidoc.element.dotenv.parse)
- description and source-code
```javascript
function parse(src) {
  var obj = {}

  // convert Buffers before splitting into lines and processing
  src.toString().split('\n').forEach(function (line) {
    // matching "KEY' and 'VAL' in 'KEY=VAL'
    var keyValueArr = line.match(/^\s*([\w\.\-]+)\s*=\s*(.*)?\s*$/)
    // matched?
    if (keyValueArr != null) {
      var key = keyValueArr[1]

      // default undefined or missing values to empty string
      var value = keyValueArr[2] ? keyValueArr[2] : ''

      // expand newlines in quoted values
      var len = value ? value.length : 0
      if (len > 0 && value.charAt(0) === '"' && value.charAt(len - 1) === '"') {
        value = value.replace(/\\n/gm, '\n')
      }

      // remove any surrounding quotes and extra spaces
      value = value.replace(/(^['"]|['"]$)/g, '').trim()

      obj[key] = value
    }
  })

  return obj
}
```
- example usage
```shell
...
The engine which parses the contents of your file containing environment
variables is available to use. It accepts a String or Buffer and will return
an Object with the parsed keys and values.

'''js
var dotenv = require('dotenv')
var buf = new Buffer('BASIC=basic')
var config = dotenv.parse(buf) // will return an object
console.log(typeof config, config) // object { BASIC : 'basic' }
'''

### Rules

The parsing engine currently supports the following rules:
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
