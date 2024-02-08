# useMemo

> It is used to memoize the output of a complex function rather than running it every single time component re-rendering takes place.

> It is also used to memorize an object when the object is used in dependency array of useEffect hook.

### Example :

#### Usage : Memorize Complex Function

```javascript
import { useMemo, useState } from 'react'

function App() {
  const [number, setNumber] = useState(1)
  const [isThemeDark, setIsThemeDark] = useState(false)
  const complexOperationValue = useMemo(() => {
    console.log('called')

    for (let i = 0; i < 100000000; i++) {}
    return '<ComplexOperationValue>'
  }, [isThemeDark])

  return (
    <div>
      <h1 className="text-5xl">{complexOperationValue}</h1>
      <p>{number}</p>
      <button
        onClick={() => {
          setNumber(previousValue => previousValue + 1)
        }}
      >
        ADD(1)
      </button>
      <br />
      <button
        className={
          isThemeDark ? 'bg-black text-white' : 'bg-white text-black'
        }
        onClick={() => setIsThemeDark(!isThemeDark)}
      >
        change my background
      </button>
    </div>
  )
}

export default App
```

#### Usage : Memorize Object For UseEffect

```javascript
import { useEffect, useMemo, useState } from 'react'

function App() {
  const [number, setNumber] = useState(0)
  const [text, setText] = useState('Light Theme')

  // const theme = { mode: 'light' }
  const theme = useMemo(() => {
    return {
      mode: 'light',
    }
  }, [text])
  // uncomment the first theme object and comment the second one and see the console. Then make it like before and see the console.

  useEffect(() => {
    console.log('Theme Changed')
  }, [theme])
  return (
    <div className="min-h-screen bg-slate-500 text-white">
      <h1 className="text-6xl">{text}</h1>
      <button
        className="my-5 ml-5 bg-blue-900 text-white p-2 rounded-md"
        onClick={() => {
          if (text === 'Light Theme') setText('Dark Theme')
          else setText('Light Theme')
        }}
      >
        Change Theme
      </button>
      <p
        className="mt-5 text-center text-3xl cursor-pointer"
        onClick={() => setNumber(prev => prev + 1)}
      >
        {number}
      </p>
    </div>
  )
}

export default App
```
