# useEffect

UseEffect is used in react function components to implement lifecycle methods.

### Example :

#### 1. Second argument types

```javascript
useEffect(() => {
  // code...
})
// If no second argument is passed,the inner code will execute on each rendering.

useEffect(() => {
  // code...
}, [])
// If empty array as 2nd argument, only run once after the first mounting or rendering.

useEffect(() => {
  // code...
}, [item1, item2])
// If array of elements is passed as second argument, the inner code will execute whenever the value of the array element changes.
```

#### 2. Behavior with change in states

```javascript
const [item1, setItem1] = useState(1)
const [item2, setItem2] = useState(2)
useEffect(() => {
  // code...
}, [item1, item2])

// on some event ---
{
  setItem1(1)
}
// This will render this component but it will not invoke the useEffect callback function as the previous value of item1 was same as the new assigned value.
```

#### 3. return function inside useEffect

```javascript
useEffect(() => {
  return () => {
    console.log('unmount')
  }
})
// The returned function will be invoked just before, whenever that component will be removed from the DOM when 2nd argument isn't provided or is an empty array.

// If there is a dependency array with elements, returned function will be called just before any other code is executed inside that useEffect callback function.
```
