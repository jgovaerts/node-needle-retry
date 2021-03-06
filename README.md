# needle-retry
[![npm version](http://img.shields.io/npm/v/needle-retry.svg)](https://www.npmjs.org/package/needle-retry)
[![Build Status](http://img.shields.io/travis/alexlangberg/node-needle-retry.svg)](https://travis-ci.org/alexlangberg/node-needle-retry)
[![Dependency Status](https://david-dm.org/alexlangberg/node-needle-retry.svg)](https://david-dm.org/alexlangberg/node-needle-retry)
[![devDependency Status](https://david-dm.org/alexlangberg/node-needle-retry/dev-status.svg)](https://david-dm.org/alexlangberg/node-needle-retry#info=devDependencies)

Combines [needle](https://www.npmjs.org/package/needle) with [retry](https://www.npmjs.org/package/retry) to account for unstable webservers. Thus, needle-retry will retry for a certain number of times (default 5) before giving up. Currently implements ```request``` and ```get```. Tests currently only cover ```GET``` requests but everything should work too, as this is basically just a wrapper.

## Installation
```
npm install needle-retry
```

## Options
Options can be passed in as the second parameter, as an object with a property ```needle``` for needle options and a property ```retry``` for retry options. This module has a single option, ```fullDocument``` that will make it retry if a full HTML document is not received. Defaults to ```false```. Default options:

```javascript
var options = {
    needleRetry: {
        fullDocument: false
    },
    needle: {
        follow_max: 20
    },
    retry: {
        retries: 5
    }
}
```

Have a look at the respective doc pages for [needle](https://www.npmjs.org/package/needle) and [retry](https://www.npmjs.org/package/retry) for a list of available options.

## Example
```javascript
var needle = require('needle-retry');

needle.get('http://www.github.com', function(error, response) {
  console.log(response.body);
});
```

## Example request
```javascript
var needle = require('needle-retry');

var options = {
    needleRetry: {
        fullDocument: false
    },
    needle: {
        follow_max: 20
    },
    retry: {
        retries: 5
    }
}

var data = {
    foo: 'bar'
}

needle.request('get', 'http://www.github.com', data, options, function(error, response) {
  console.log(response.body);
});
```
