## API

```js
const rematchStatePlugin = require('rematch-state-plugin')
```

### add plugin entry

```js
import {init} from '@rematch/core'

const store = init({
  modules: {foo, bar},
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
