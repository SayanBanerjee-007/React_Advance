# useCallback

It is used to memorize a function and it returns the given function as a callback. It only recreate the function if the given function dependencies changes.

### Example:

#### ./App.jsx

```javascript
import { useCallback, useState } from 'react'
import List from './components/List'

function App() {
  const [input, setInput] = useState(0)
  const [theme, setTheme] = useState('light')

  // const getItems = () => {
  //   console.log('getItems() called')
  //   return [input, input + 1, input + 2]
  // }

  const getItems = useCallback(() => {
    console.log('getItems() called')
    return [input, input + 1, input + 2]
  }, [input])

  return (
    <div className={theme === 'light' ? 'bg-slate-500' : 'bg-black'}>
      <input
        type="number"
        value={input}
        onChange={e => setInput(Number(e.target.value))}
      />
      <br />
      <button
        className="bg-blue-600 text-white m-2 p-2 rounded-lg"
        onClick={() => {
          theme === 'light' ? setTheme('dark') : setTheme('light')
        }}
      >
        Toggle Theme
      </button>
      <p className="text-white text-lg">Next Three Numbers:</p>
      <List getItems={getItems} />
    </div>
  )
}

export default App
```

#### ./components/List.jsx

```javascript
// Two choices:
// 1. use React.memo to memoize the getItems method
// 2. use useEffects to rerun getItems method when it is changed

// 1 =================================

import React from 'react'
function List({ getItems }) {
  return getItems().map((item, index) => (
    <div
      key={index}
      className="text-white"
    >
      {item}
    </div>
  ))
}
export default React.memo(List)

// 2 =================================

// import { useEffect, useState } from 'react'
// function List({ getItems }) {
//     const [items, setItems] = useState([])

//     useEffect(() => {
//       console.log('useEffect() called')
//       setItems(getItems())
//     }, [getItems])

//     return items.map((item, index) => (
//       <div
//         key={index}
//         className="text-white"
//       >
//         {item}
//       </div>
//     ))
// }
// export default List
```
