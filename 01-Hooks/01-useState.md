# useState

UseState is one of the most popular react hook. It allows functional components to manage state.

### Example :

#### 1. Types of calling the useState method

```javascript
function complexFunction() {
  // This function performs some complex operations
  return 'result'
}

const [value, setValue] = useState(123) // 123 is set as value during the first render only

const [value2, setValue2] = useState(() => {
  // some complex operations
  return 'result'
}) // The result is set as value during the first render only and here the callback function is called only for the very first rendering.

const [value3, setValue3] = useState(complexFunction) //complexFunction is called every time this component renders as for each render a new function is created. So don't use this until the function isn't much complex.
```

#### 2. Types of using the set method given by useState

```javascript
let newValue = 23
setValue(newValue) // If the value to be set is different from the previous value then use this way

setValue(() => {
  return value + 1
}) // If the value to be set is dependent upon the previous value then use this callback function way

// Let the value be 0 at this point for the bellow example
setValue(value + 2)
setValue(value + 2)
setValue(value + 2)
setValue(value + 2)
// Here the value = 2 not (2 + 2 + 2 + 2) = 8 as react does not set the value individually, it groups the values together and as all  are the same it will add only 2 to the value. If callback function is used in setValue then the value will be 8
```

#### 3. Behavior with object as value

```javascript
const [obj, setObj] = useState({
  name: 'Goku',
  age: 123,
})

setObj({ age: 1266 }) // This changes the whole object and now the object is only {age: 1266} as this create a new object and react compare the new object with the old one and as both are different it will save the new one and old one is garbage collected if it has no reference left in the background.
```
