# Fingerprintjs2.1


Original fingerprintjs library was developed in 2012, it's now impossible to evolve it
without breaking backwards compatibilty, so this project will be where
all the new development happens.

This project will use significantly more sources for fingerprinting, all
of them will be configurable, that is it should be possible to
cherry-pick only the options you need or just enable them all.

I'm also paying special attention to IE plugins, popular in China, such
as QQ, Baidu and others.

This project will not be backwards compatible with original
fingerprintjs.

This project uses `semver`.



### Usage


```js
var options = {swfPath: '/assets/FontList.swf', excludeUserAgent: true};
new Fingerprint2(options).get(function(result){
  console.log(result);
});
```

Full list of options will be in the
(https://github.com/Valve/fingerprintjs2/wiki/List-of-options) wiki
page.

Flash font enumeration is disabled by default. JS code is used by
default to get the list of available fonts.

The reason for this  is that Flash will not work in incognito mode.

However, you can make the library to use Flash when detecting the fonts
with:

```js
excludeJsFonts: true
```
option.

To use Flash font enumeration, make sure you have swfobject available.
If you don't, the library will skip the Flash part entirely.

#### `detectScreenOrientation` option is `true` by default

To ensure consistent fingerprints when users rotate their mobile
devices.



### List of fingerprinting sources

1. UserAgent
2. Language
3. Color Depth
4. Screen Resolution
5. Timezone
6. Has session storage or not
7. Has local storage or not
8. Has indexed DB
9. Has IE specific 'AddBehavior'
10. Has open DB
11. CPU class
12. Platform
13. DoNotTrack or not
14. Full list of installed fonts (maintaining their order, which increases the entropy), implemented with Flash.
15. A list of installed fonts, detected with JS/CSS (side-channel technique) - can detect up to 500 installed fonts without flash
16. Canvas fingerprinting
17. WebGL fingerprinting
18. Plugins (IE included)
19. Is AdBlock installed or not
20. Has the user tampered with its languages <sup>[1](https://github.com/Valve/fingerprintjs2/wiki/Browser-tampering)</sup>
21. Has the user tampered with its screen resolution <sup>[1](https://github.com/Valve/fingerprintjs2/wiki/Browser-tampering)</sup>
22. Has the user tampered with its OS <sup>[1](https://github.com/Valve/fingerprintjs2/wiki/Browser-tampering)</sup>
23. Has the user tampered with its browser <sup>[1](https://github.com/Valve/fingerprintjs2/wiki/Browser-tampering)</sup>
24. Touch screen detection and capabilities
25. Pixel Ratio
26. System's total number of logical processors available to the user agent.
27. [Device memory](https://w3c.github.io/device-memory/)


By default, JS font detection will only detect up to 65 installed fonts. If you want to improve the font detection,
you can pass `extendedJsFonts: true` option. This will increase the number of detectable fonts to ~500.

On my machine (MBP 2013 Core i5) + Chrome 46 the default FP process takes about 80-100ms. If you use `extendedJsFonts` option this time will increase up to 2000ms (cold font cache).
This option can incur even more overhead on mobile Firefox browsers, which is much slower in font detection, so use it with caution on mobile devices.

To speed up fingerprint computation, you can exclude font detection (~ 40ms), canvas fingerprint (~ 10ms), and WebGL fingerprint (~ 35 ms).

### Many more fingerprinting sources will be implemented, such as
(in no particular order)

* Multi-monitor detection,
* Internal HashTable implementation detection
* WebRTC fingerprinting
* Math constants
* Accessibility fingerprinting
* Camera information
* DRM support
* Accelerometer support
* Virtual keyboards
* List of supported gestures (for touch-enabled devices)
* Pixel density
* Video and audio codecs availability
* Audio stack fingerprinting

#### To recompile the `FontList.swf` file:

* Download [Adobe Flex SDK](http://www.adobe.com/devnet/flex/flex-sdk-download.html)
* Unzip it, add the `bin/` directory to your `$PATH`  (mxmlc binary should be in path)
* Run `make`

#### My talk about the library (in Russian) on FrontEnd Conf 2015

https://player.vimeo.com/video/151208427

#### License: MIT or Apache, whichever you prefer.
