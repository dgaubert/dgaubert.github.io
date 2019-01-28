---
title:  "Refactor: change reference to value"
---

## Overview

Before:
```js
class Engine {
  constructor () {
    this._status = new Status(false)
  }

  get status () {
    return this._status
  }

  start () {
    this._status.value = true
    return this._status
  }

  stop () {
    this._status.value = false
    return this._status
  }
}

class Status {
  constructor (value) {
    this._value = value
  }

  get value () {
    return this._value
  }

  set value (value) {
    this._value = value
  }
}
```

After:
```js
class Engine {
  constructor () {
    this._status = new Status(false)
  }

  get status () {
    return this._status
  }

  start () {
    this._status = new Status(true)
    return this._status
  }

  stop () {
    this._status = new Status(false)
    return this._status
  }
}

class Status {
  constructor (value) {
    this._value = value
  }

  get value () {
    return this._value
  }

  set value (value) {
    this._value = value
  }
}
```

The goal is to provide an immutable value for engine's status. Useful in distributed systems when you ask the engine's status and the value that you already got won't change even if another actor changes engine's status.
