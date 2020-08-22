<!-- AUTO_GENERATED_UNTOUCHED_FLAG -->

# rematch-state-plugin

> use `state` &amp; `setState` in rematch effects

[![Build Status](https://img.shields.io/travis/magicdawn/rematch-state-plugin.svg?style=flat-square)](https://travis-ci.org/magicdawn/rematch-state-plugin)
[![Coverage Status](https://img.shields.io/codecov/c/github/magicdawn/rematch-state-plugin.svg?style=flat-square)](https://codecov.io/gh/magicdawn/rematch-state-plugin)
[![npm version](https://img.shields.io/npm/v/rematch-state-plugin.svg?style=flat-square)](https://www.npmjs.com/package/rematch-state-plugin)
[![npm downloads](https://img.shields.io/npm/dm/rematch-state-plugin.svg?style=flat-square)](https://www.npmjs.com/package/rematch-state-plugin)
[![npm license](https://img.shields.io/npm/l/rematch-state-plugin.svg?style=flat-square)](http://magicdawn.mit-license.org)

## Install

```sh
$ npm i -S rematch-state-plugin
```

## API

```js
const rematchStatePlugin = require('rematch-state-plugin')
```

### add plugin entry

```js
import {init} from '@rematch/core'

const store = init({
  models: {foo, bar},
  plugins: [rematchStatePlugin()],
})
```

#### plugin create options

```js
const {state, setState, setStateAction} = {
  state: 'state',
  setState: 'setState',
  setStateAction: '__rematch_state_plugin_@@_set_state__',
}
```

### use `this.state` & `this.setState` in effects

```js
// models/count.js with this plugin enabled
export default {
  state: {
    val: 1,
  },

  effects: {
    add() {
      this.setState({val: this.state.val + 1})
    },
  },
}
```

```js
// models/count.js without this plugin enabled
export default {
  name: 'count',

  state: {
    val: 1,
  },

  setState(payload) {
    return {...state, ...payload}
  },

  effects: {
    add(payload, rootState) {
      const nsp = 'count'
      const {val} = rootState[nsp]
      this.setState({val: val + 1})
    },
  },
}
```

## Changelog

[CHANGELOG.md](CHANGELOG.md)

## License

the MIT License http://magicdawn.mit-license.org
