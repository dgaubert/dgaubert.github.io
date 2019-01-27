---
title:  "Refactor: change reference to value"
---

## Overview

Before:
```js
class Engine {
  constructor () {
    this._on = false
  }

  get status () {
    return this._on
  }

  start () {
    this._on = true
    return this._on
  }

  stop () {
    this._on = true
    return this._on
  }
}
```

After:
```js
class Engine {
  constructor () {
    this._status = new Status({ value: false })
  }

  get status () {
    return this._status.value
  }

  start () {
    this._status = new Status({ value: true })
    return this._status.value
  }

  stop () {
    this._status = new Status({ value: false })
    return this._status.value
  }
}

class Status {
  constructor (value) {
    this._value = value
  }

  get value () {
    return this._value
  }
}
```

The goal is to provide an immutable value for engine's status. Useful in distributed systems when you ask the engine's status and the value that you already got won't change even if another actor changes engine's status.
