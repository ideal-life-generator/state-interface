# state-interface

## Installation

```bash
$ npm install state-interface --save
```

## Usage

```js
import {
  ADD_USER,
  REMOVE_USER,
  SWITCH_USER
} from "actions/users"
import initialStateInterface from "interfaces/users"

export default function users (state = initialStateInterface, action) {
  switch (action.type) {
    case ADD_USER:
      return state.update((state) => {
        return state.addUser(action.user)
      })
    case REMOVE_USER:
      return state.update((state) => {
        return state.removeUser(action.id)
      })
    case SWITCH_USER:
      return state.update((state) => {
        return state
          .removeUser(action.id)
          .addUser(action.user)
      })
    default:
      return state
  }
}
```

Don't care about what returns in update, each state is unique.

## Interfaces

```js
import stateInterface from "state-interface"

const initialState = {
  users: [ ],
  count: 0
}

class UsersInterface {
  addUser (user) {
    this.users.push(user)

    return this.updateCount()
  }

  removeUser (id) {
    const userIndex = this.users.findIndex((user) => user.id === id)

    this.users.splice(userIndex, 1)

    return this.updateCount()
  }

  updateCount () {
    this.count = this.users.length

    return this
  }
}

export default stateInterface(Users, initialState)
```

---

## See also

[![Red Hot Chili Peppers - Californication - Live at Slane Castle ](http://i.imgur.com/aHhgwQi.png)](https://www.youtube.com/watch?v=Z0AXjUy1_gY)