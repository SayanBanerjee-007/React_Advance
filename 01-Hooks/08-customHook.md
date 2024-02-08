# Custom Hooks

Any function that is using any of the react in built hooks and if the function's name starts with 'use' then it will be called custom hook.

### Example:

#### ./App.jsx

```javascript
import useLocalStorage from './hooks/useLocalStorage'

function App() {
  const [value, setValue] = useLocalStorage('input', '')
  return (
    <div>
      <input
        type="text"
        value={value}
        onChange={e => setValue(e.target.value)}
      />
    </div>
  )
}

export default App
```

#### ./hooks/useLocalStorage.js

```javascript
import { useEffect, useState } from 'react'

function getSavedValues(key, value) {
  const savedValues = localStorage.getItem(key)
  if (savedValues) return JSON.parse(savedValues)
  return value
}
function setSavedValues<valueType>(key, value) {
  localStorage.setItem(key, JSON.stringify(value))
}
export default function useLocalStorage<initialValueType>(
  key,
  initialValue
) {
  const [value, setValue] = useState(() => {
    return getSavedValues(key, initialValue)
  })
  useEffect(() => {
    setSavedValues(key, value)
  }, [value])
  return [value, setValue]
}
```
