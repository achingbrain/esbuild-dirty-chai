# loading dirty-chai in esbuild

This broke between `esbuild@0.11.10` and `esbuild@0.11.11`

`index.js` contains one line:

```js
const d = require('dirty-chai')
```

This throws an error with `esbuild@0.11.11` but does not with `esbuild@0.11.10`

This may be related to how `dirty-chai` does environment detection - https://github.com/ipfs/js-ipfs-unixfs/pull/116#issuecomment-825646616

## To replicate

1. Clone and build

```console
$ git clone https://github.com/achingbrain/esbuild-dirty-chai.git
$ cd esbuild-dirty-chai
$ npm i
$ npm run build
$ open index.html
```

2. Look in the browser console

```
index.js:1 Uncaught ReferenceError: chai is not defined
    at index.js:1
    at index.js:1
    at index.js:1
    at index.js:1
    at index.js:1
```

3. Build using older version

```console
$ npm install esbuild@0.11.10
$ npm run build
$ open index.html
```

No errors will be in the browser console.
