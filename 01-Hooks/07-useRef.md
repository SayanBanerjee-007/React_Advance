# useRef

It is used to create a variable that maintains its state in between rendering and also does't trigger rendering like state variables when the value is changed.

### Example :

#### ./App.jsx

```javascript
import { useEffect, useRef, useState } from 'react'

// const previousName = { current: '' } // useRef is similar to this declaration
function App() {
  const [name, setName] = useState('')
  const previousName = useRef('')
  const inputRef = useRef()

  console.log(inputRef)

  useEffect(() => {
    previousName.current = name
  }, [name])

  useEffect(() => {
    inputRef.current.focus()
  }, [])

  return (
    <div>
      <input
        type="text"
        value={name}
        onChange={e => setName(e.target.value)}
        placeholder="Enter your name"
        ref={inputRef}
      />
      <p className="text-white">Now the input text is : {name}</p>
      <p className="text-white">
        Previously the input text was: {previousName.current}
      </p>
    </div>
  )
}

export default App
```
