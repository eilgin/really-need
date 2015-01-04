First call to `require('really-need')` replaced `Module.prototype.require` with a better version.
Other modules can use new `require` directly. The module making the call to `really-need` needs
to use the returned value.

```js
require = require('really-need');
// global require is now a better one!
// evaluate foo.js again, busting the cache
var foo = require('./foo', {
    // remove previously loaded foo module
    bustCache: true,
    // remove from cache AFTER loading
    cache: false,
    pre: function (source, filename) {
        // transform the source before compiling it
        return source;
    },
    post: function (exported, filename) {
        // transform the exported object / value from the file
        return exported;
    }
});
```