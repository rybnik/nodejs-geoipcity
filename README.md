geoipcity for node.js
=====================

Lookup details for an IP using the [Maxmind GeoIP City](http://www.maxmind.com/app/web_services) webservice. This requires a license key with webservice access.

[![Build Status](https://secure.travis-ci.org/fvdm/nodejs-geoipcity.png?branch=master)](http://travis-ci.org/fvdm/nodejs-geoipcity)

## Install

### With NPM

**npm install geoipcity**

```js
var geoip = require('geoipcity');
```

### From source:

```js
var geoip = require('./geoipcity.js');
```

## Example

```js
var geoip = require('geoipcity');

geoip.settings.license = 'licenseKey';

geoip.lookup( '8.8.8.8', function(data) {
  console.log( data.city );
  console.log( data.latitude +', '+ data.longitude );
});
```

```js
{ target:      '8.8.8.8',
  countryCode: 'US',
  regionCode:  'CA',
  city:        'Mountain View',
  postalCode:  '94043',
  latitude:    '37.419201',
  longitude:   '-122.057404',
  metroCode:   '807',
  areaCode:    '650',
  isp:         'Level 3 Communications',
  org:         'Google Incorporated' }
```

## Unlicense

This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <http://unlicense.org>
