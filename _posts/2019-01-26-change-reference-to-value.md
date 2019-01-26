---
title:  "Refactor: change reference to value"
---

## Overview

Before:
```js
class Car {
    constructor (speed) {
        this._speed = speed
    }

    slowDown (amount) {
        this._speed -= amount
    }
}
```

After:
```js
class Car {
    constructor (speed) {
        this._speed = new Speed(amount)
    }

    slowDown (amount) {
        this._speed -= new Speed(amount)
    }
}

class Speed {
    constructor (amount) {
        this._amount = amount
    }
}
```
