# useReducer

It is used to manage lots of states without using the useState function. More useful for managing state of type objects or arrays.

### Example :

#### ./App.js

```javascript
import { useReducer } from 'react'

const ACTIONS = {
  DECREMENT: 'decrement',
  INCREMENT: 'increment',
}

const reducer = (state: any, action: any) => {
  switch (action.type) {
    case ACTIONS.DECREMENT:
      return { number: state.number - action.payload }
    case ACTIONS.INCREMENT:
      return { number: state.number + action.payload }
    default:
      return state
  }
}
function App() {
  const [state, dispatch] = useReducer(reducer, { number: 7 })

  return (
    <div className="text-white text-4xl pt-20 flex items-center justify-center">
      <button
        className="bg-blue-600 rounded-md p-2 m-2"
        onClick={() =>
          dispatch({ type: ACTIONS.DECREMENT, payload: 2 })
        }
      >
        -2
      </button>
      <h1>{state.number}</h1>
      <button
        className="bg-blue-600 rounded-md p-2 m-2"
        onClick={() =>
          dispatch({ type: ACTIONS.INCREMENT, payload: 4 })
        }
      >
        +4
      </button>
    </div>
  )
}

export default App
```

### Polyfill of useReducer :

```javascript
import { useState } from 'react'

function useMyReducer(reducerFunction, initialValue) {
  const [value, setValue] = useState(initialValue)
  function dispatch(...args: any) {
    const result = reducerFunction(value, ...args)
    console.log(result)

    setValue(result)
  }
  return [value, dispatch]
}
```
