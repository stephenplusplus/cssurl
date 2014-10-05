[![Build Status](https://travis-ci.org/nzakas/css-url-rewriter.png?branch=master)](https://travis-ci.org/box/leche)

# CSS URL Rewriter

There are many reasons why you would want to systematically replace URLs in CSS code: to convert them into data URIs, to point them to a CDN, to replace a filename with an auto-generated one, and so on. This utility helps by parsing out the URLs in a given string of CSS code and allowing you to replace them with any value you choose. The resulting CSS code is exactly the same as the original except that the URLs have been replaced according to your preferences.

## Usage

```js
var CSSURLRewriter = require("css-url-rewriter");

var rewriter = new CSSURLRewriter(function(url) {
    // automatically append a query string with a unique value to bust caches
    return url + "?v=" + Date.now();
});

var result = rewriter.rewrite(cssCode);
```

As the CSS URL Rewriter goes through the CSS code, it will call the function passed to the `CSSURLRewriter` constructor and pass in each URL that it finds. The `url` is the URL as found in the CSS code with any quotes and surrounding whitespace removed (it does *not* contain the `url()`). You can then inspect the URL, modify it however you want, and return the value you want to use in its place.

## Limitations

The CSS URL Rewriter will only replace URLs represented as URL tokens, that means it must be in the form `url(foo.css)` and not just `"foo.css"`, as is allowed in some parts of CSS.

## Copyright and License (BSD3)

Copyright 2014 Nicholas C. Zakas. All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.