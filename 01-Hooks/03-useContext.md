# useContext

It is used to get access to the to a particular context by providing the context. Context API is a built-in hook in react that allows you to manage the states globally and access the context from any component without using prop drilling.

### Example :

```javascript
import { useState, useContext, createContext } from 'react'

// Creating Context
const CountContext = createContext({})

// Context Provider
const CountContextProvider = ({ children }) => {
  const [number, setNumber] = useState(0)
  return (
    <CountContext.Provider value={{ number, setNumber }}>
      {children}
    </CountContext.Provider>
  )
}

// Custom Hooks
const useCount = () => useContext(CountContext)

// Exports
export { CountContext, CountContextProvider, useCount }
```
