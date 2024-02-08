# Life Cycle Method

## Definition :

In React, the lifecycle methods are special methods that are invoked at various stages during the lifecycle of a component. These methods allow developers to execute code at specific points in a component's existence, such as when it is being created, updated, or destroyed. It is only used in Class components.

<a href='https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/' style="display:flex "><img width="20" height="20" style="margin-right:.5rem" src="https://img.icons8.com/flat-round/64/link--v1.png" alt="link--v1"/>Cycle Method Diagram</a>

## Example :

In the following example componentDidMount, componentDidUpdate, and componentWillUnmount are used which are used mostly.

```javascript
import React from 'react'

class Timer extends React.Component {
  constructor(props: any) {
    super(props)
    this.state = {
      time: new Date(),
    }
    const a = 11
  }
  updateTime = () => {
    this.setState({ time: new Date() })
  }
  componentDidMount(): void {
    this.timerId = setInterval(this.updateTime, 1000)
  }
  componentWillUnmount(): void {
    clearInterval(this.timerId)
  }
  render() {
    return (
      <div>
        <p>Timer: {this.state.time.toLocaleString()}</p>
      </div>
    )
  }
}
class Number extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      number: 1,
      val: 100,
    }
  }
  componentDidUpdate(
    prevProps: Readonly<{}>,
    prevState: Readonly<{}>,
    snapshot?: any
  ): void {
    if (prevState.number !== this.state.number) {
      this.setState({ val: prevState.val * 2 })
    }
  }
  render() {
    return (
      <div className="flex flex-col items-center">
        <p>Value:{this.state.val}</p>
        <p>{this.state.number}</p>
        <button
          className="bg-blue-600 p-1 rounded-md block text-center"
          onClick={() => {
            this.setState({ number: this.state.number + 1 })
          }}
        >
          Click me
        </button>
      </div>
    )
  }
}

const App = () => {
  return (
    <div className="text-white flex flex-col justify-center items-center pt-24 text-2xl">
      <Timer />
      <Number />
    </div>
  )
}

export default App
```

## Lifecycle Methods in Sequential Manner

\_\_React lifecycle methods are invoked in a specific sequence during the different phases of the component's life. Here's an overview of the main lifecycle methods and their execution sequence:

### 1. Mounting Phase:

**constructor(props) :**

> This is the first method called when a component is created. It is used for initializing state and binding event handlers.

**static getDerivedStateFromProps(nextProps, prevState) :**

> Invoked right before rendering when new props or state are being received. It returns an object to update the state or null to indicate that the new props do not require any state updates.

**render() :**

> This method is responsible for rendering the component's UI. It should be a pure function without side effects.

**componentDidMount() :**

> Invoked immediately after the component is inserted into the DOM. It is often used for tasks like data fetching, setting up subscriptions, or manually changing the DOM.

### 2. Updating Phase:

**static getDerivedStateFromProps(nextProps, prevState) :**

> Similar to the mounting phase, this method is called before every render during the update phase.

**shouldComponentUpdate(nextProps, nextState) :**

> This method allows you to control if the component should re-render or not based on changes in props or state. It returns a boolean value indicating whether the component should update.

**render() :**

> Re-renders the component with updated props and state.

**getSnapshotBeforeUpdate(prevProps, prevState) :**

> Called just before the changes from the virtual DOM are to be reflected in the actual DOM. It allows the component to capture some information (e.g., scroll position) before the update.

**componentDidUpdate(prevProps, prevState, snapshot) :**

> Invoked after the component has been updated in the DOM. It is often used for performing side effects, like interacting with the DOM or making network requests.

### 3. Unmounting Phase:

**componentWillUnmount() :**

> Invoked just before the component is unmounted and destroyed. It is used for cleanup tasks like canceling network requests, clearing up subscriptions, or cleaning up resources.
