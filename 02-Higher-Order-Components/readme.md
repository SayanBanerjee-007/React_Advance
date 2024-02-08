# Higher Order Components

### Definition :

A Higher Order Component (HOC) is a function that takes a component and returns a new component with enhanced functionality or additional props. Essentially, it's a way to reuse component logic and share it across different parts of your application.

### Why use Higher Order Components?

**Reusability:** HOCs promote code reuse by encapsulating common logic in a separate function. This helps in avoiding code duplication across different components.

**Abstraction:** They allow you to abstract away complex logic or behavior, making your components more focused and easier to understand.

**Composition:** HOCs facilitate the composition of multiple behaviors into a single component. You can apply multiple HOCs to a component to aggregate different functionalities.

**Separation of Concerns:** By moving certain aspects of a component's behavior (like data fetching or state management) into an HOC, you can achieve a cleaner separation of concerns.

### When to use Higher Order Components?

**Common Logic:** If you find yourself repeating the same logic in multiple components, consider extracting that logic into an HOC.

**Cross-Cutting Concerns:** HOCs are useful for handling cross-cutting concerns such as logging, authentication, or data fetching.

**Code Organization:** When you want to improve the organization of your code by isolating specific functionalities into reusable units.

**Decorator Pattern:** If you're familiar with the decorator pattern from object-oriented design, HOCs follow a similar concept by wrapping a component with additional functionality.

### Example :

```javascript
import { useState } from 'react'

function withLazyLoading(WrappedComponent) {
  return function (props) {
    const [loading, setLoading] = useState(true)
    setTimeout(function () {
      setLoading(false)
    }, 2000)
    return (
      <div className="text-white flex justify-center">
        {loading ? 'Loading...' : <WrappedComponent />}
      </div>
    )
  }
}
function component() {
  return (
    <div>
      <p className="text-5xl m-10">Welcome to LOL 1</p>
      <p className="text-5xl m-10">Welcome to LOL 2</p>
      <p className="text-5xl m-10">Welcome to LOL 3</p>
    </div>
  )
}
function App() {
  const ComponentWithLazyLoading = withLazyLoading(component)
  return (
    <div>
      <ComponentWithLazyLoading />
    </div>
  )
}

export default App
```
