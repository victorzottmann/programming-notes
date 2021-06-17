# State and Lifecycle Methods

### State

**Important:** notes about state to be added.

```jsx
import React, { Component } from 'react'
import Clock from './Clock'

class App extends Component {
  constructor(props) {
    super(props)
    this.state = { latitude: null, errorMessage: "" }
    
    window.navigator.geolocation.getCurrentPosition(
      position => this.setState({ latitude: position.coords.latitude }),
      error => this.setState({ errorMessage: error.message })
    )
    
    this.isItWarm = this.isItWarm.bind(this)
    this.getClockIcon = this.getClockIcon.bind(this)
 	}
  
  isItWarm() {
    const { latitude } = this.state
    const month = new Date().getMonth()
    
    if (((month > 4 && month < 9) && latitude > 0) || ((month <= 4 || month > 9) && latitude > 0) || latitude === 0) {
      return true
    }
    return false
  }
  
  getClockIcon() {
    if (this.isItWarm()) {
      return "summer.png"
    }
    return "winter.png"
  }
  
  render() {
    const { latitude, errorMessage } = this.state
    return (
    	<div>
      	<h1>{latitude}</h1>
        {errorMessage || <Clock date={new Date()}} />}
      </div>
    )
  }
}

export default App
```

### Lifecycle Methods

- **componentDidMount**

  Runs after the first re-render; it's the best place to make API calls.

- **componentDidUpdate**

  Runs after subsequent renders (not on the first render), provided that the `prevState` is different to the `newState`. If there are any repetitive tasks, this would be the best place to put them (like `setInterval`).

  It takes two arguments: `componentDidUpdate(prevProps, prevState)`

- **componentWillUnmount**

  Runs at the end of a component's lifecycle; it clears any background tasks that are running for a given component (like `clearInterval`).