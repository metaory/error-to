ERROR-TO
========

<div align=center>
  <h3>🚧 WIP 🚧</h3>
</div>

<div align=center>
  <img alt="logo-of-error-ro" src="https://raw.githubusercontent.com/metaory/error-to/master/.github/assets/logo.png" width="70%">
  <h2>🚧 Serialize Errors to</h2>
  <h5>🚧 Transform to Array / Object</h5>
  ╶─╴╶╴╶╴╶╴╶╴╶╴╶╴╶╴╶╴╶╴╶─╴
</div>

---

♻️ Serialize an error into a short object or array with customizable formatter

---

- 🎌 Short Readable formats
- 🧬 Custom formatters
- 📦 Zero Dependency
- 🌐 Works in ESM & CJS
- 〽️ Minimal Obsessive Disorder

---

<br>
<br>

Options
-------
- `toArray`?: transform to array
- `join`?: the separator character
- `withKeys`?: prefix with keys
- `withStack`?: whether to include stack 🚧

```js
errorTo(new Error('xyzzy', cause: new SyntaxError('hoge')), {
  toArray: true, // result in array output
  join: '::', // whether to concat values with value as separator
  withKeys: true, // whether to prefix keys to each value
})
```

Usage
-----
```sh
# install
npm install error-to
```
```js
// ESM
import errorTo from 'error-to'

// CJS
const errorTo = require('error-to')

const { log } = console

// ═══════════════════════

// ┍━━━━━━━━━━━━━━━━━━━━━┑
// └─── SIMPLE ERRORS ───┘

const e1 = new Error('xyzzy')

// :: Plain Object
log(error-to(e1))
// { name: 'Error', message: 'xyzzy' }

// :: Plain Array
log(error-to(e1, { toArray: true }))
// ['Error', 'xyzzy']

// :: Joined Array
log(error-to(e1, { toArray: true, join: '::' }))
// ['Error::xyzzy']

// :: Plain Array with Keys
log(error-to(e1, { toArray: true, withKeys: true }))
// ['name:Error', 'message:xyzzy']

// :: Joined Array with Keys
log(error-to(e1, { toArray: true, withKeys: true, join: '__' }))
// ['name:Error__message:xyzzy']

// ════════════════════

// ┍━━━━━━━━━━━━━━━━━━┑
// └─── WITH CAUSE ───┘
const e2 = new SyntaxError('hoge', { cause: e1 })

// :: Plain Object with Cause
log(error-to(e2))
// { name: 'SyntaxError', message: 'hoge', cause: { name: 'Error', message: 'xyzzy' } }

// :: Plain Array with Cause
log(error-to(e2, { toArray: true }))
// ['SyntaxError', 'hoge', ['Error', 'xyzzy']]

// :: Joined Array with Cause
log(error-to(e2, { toArray: true, join: '::' }))
// ['SyntaxError::hoge', 'Error::xyzzy']

// :: Plain Array with Cause and Keys
log(error-to(e2, { toArray: true, join: withKeys: true }))
// ['name:SyntaxError', 'message:hoge', 'cause.name:Error', cause.message:'xyzzy']

// :: Joined Array with Cause and Keys
log(error-to(e2, { toArray: true, join: withKeys: true, join: '__' }))
// ['name:SyntaxError__message:hoge__cause.name:Error__cause.message:xyzzy']


// ═══════════════════════

// ┍━━━━━━━━━━━━━━━━━━━━━┑
// └── AggregateError ───┘
const e3 = new AggregateError([e1, new Error('frob'), e2], 'nyoro')

// :: Plain Object on AggregateError
log(error-to(e3))
/*
  {
    name: 'AggregateError',
    message: 'nyoro',
    errors: [
      { name: 'Error', message: 'xyzzy' },
      { name: 'Error', message: 'frob' },
      { name: 'SyntaxError', message: 'nyoro' },
    ]
  }
*/


// :: Plain Array on AggregateError
// TODO::WRITE:DOC::

// :: Joined Array with Cause on AggregateError
// TODO::WRITE:DOC::

// :: Plain Array with Cause and Keys on AggregateError
// TODO::WRITE:DOC::

// :: Joined Array with Cause and Keys on AggregateError
// TODO::WRITE:DOC::


// TODO::
// 'Error:no such file or directory:ENOENT:-2:nada'
// a1 = ['Error', 'no such file or directory', 'ENOENT', '-2', 'nada']
// a2 = ['name:Error', 'message:no such file or directory', 'code:ENOENT', 'errno:-2', 'path:nada']


```
TODO
----

---

License
-------
[MIT](LICENSE)
