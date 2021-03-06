geoipcity for node.js
=====================

Lookup details for an IP using the [Maxmind GeoIP City](http://www.maxmind.com/en/web_services) webservices. This requires a license key with webservice access.

This module is compatible with the following Maxmind services:

* Country
* City
* City/ISP/Org
* Omni

You can configure a service to use for all lookups or decide per lookup which service you'd like to use. This allows you to use less expensive calls depending on the level of detail required. See [Configuration](#configuration) and [.lookup](#lookup) below for more information.


Installation
------------

### With NPM

This is always the most recent *stable* version.

	npm install geoipcity


### From Github:

This is the most recent code, but may be *untested*.

	git clone https://github.com/fvdm/nodejs-geoipcity
	npm install ./nodejs-geoipcity


Configuration
-------------

You can change a few parameters with the `settings` object:

	name        default             description
	
	license                         Your MaxMind license key
	service     cityisporg          API webservice: omni, country, city, cityisporg
	apihost     geoip.maxmind.com   API servername
	apiproto    http                Protocol: http or https
	


### Example

```js
geoip.settings.license = 'myLicenseKey'
geoip.settings.apiproto = 'https'
```


.lookup ( ip, [service], callback )
-----------------------------------

Retrieve geolocation and related information about an IP-address from the Maxmind API.


	ip         string     required   IPv4 or IPv6 address to lookup
	
	service    string     optional   Which webservice to use:
	                                 omni, country, city, cityisporg (default)
	                                 Override the default with 'settings.service'
	                                 
	callback   function   required   A function to receive the data:
	                                 callback ( err, [data] )


* Make sure to first set the license key.

* The `callback` function takes these two parameters: first `err` then `data`. In case of a problem `err` is an `instanceof Error` with all related information. When everything is good, `err` is *null* and `data` contains the *object* with geo data.


### Example

```js
var geoip = require('geoipcity')

geoip.settings.license = 'licenseKey'

geoip.lookup( '8.8.8.8', function( err, data ) {
	if( !err ) {
		console.log( data.city )
		console.log( data.latitude +', '+ data.longitude )
	} else {
		console.log( err )
		console.log( err.stack )
	}
})
```


### Output for service `cityisporg`

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


Error handling
--------------

The `err` parameter in the callback function can return these errors. Some have additional properties.

### Errors

	Error: No license         You did not specify your license key.
	Error: Invalid IP         The provided IP address is invalid.
	Error: Invalid service    The provided service name is invalid.
	Error: Request failed     The request can't be made.
	Error: HTTP error         The API returned a HTTP error.
	Error: No response        The API did not return data.
	Error: Invalid response   The API returned invalid data.
	Error: Disconnected       The API closed the connection too early.
	Error: API error          The API returned an error.

### Additional properties

	.details       ie. IP_NOT_FOUND
	.httpCode      ie. 404
	.httpHeaders   Object with response headers
	.request       Object with request details
	.response      Response body


Unlicense
---------

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
