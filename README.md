# React-Conditional-Rendering

in `React` you can create `distinct` components that encapsulate behaviour you need. Then you can render only some of them. depending on the `state` of your application.

## isLoggedIn Example

LoginButton.js
```js
import React from 'react'

export default function LoginButton({ setIsLoggedIn }) {
  return (
    <button onClick={() => setIsLoggedIn(true)}>Login</button>
  )
}
```

LogoutButton.js
```js
import React from 'react'

export default function LogoutButton({ setIsLoggedIn }) {
  return (
    <button onClick={() => setIsLoggedIn(false)}>Logout</button>
  )
}
```

UserGreeting.js
```js
import React from 'react';

export default function UserGreeting() {
  return <h1>Welcome Back!</h1>
}
```

GuestGreeting.js
```js
import React from 'react';

export default function GuestGreeting() {
  return <h1>Please Signup</h1>
}
```

Greeting.js
```js
import React from 'react'
import UserGreeting from './UserGreeting'
import GuestGreeting from './GuestGreeting'

export default function Greeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <UserLoggedIn />
  } 
  
  return <GuestLoggedIn />
}
```

App.js
```js
import { useState } from 'react'
import LoginButton from './LoginButton'
import LogoutButton from './LogoutButton'
import Greeting from './Greeting'

export default function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false)
  
  return (
    <div>
      <nav>
        <LoginButton setIsLoggedIn={setIsLoggedIn} />
        <LogoutButton setIsLoggedIn={setIsLoggedIn} />
      </nav>
      <Greeting isLoggedIn={isLoggedIn} />
    </div>
  )
}
```


## Element Variables

You can use `variables` to store `elements`. This can help you conditionally render a part of the component while the rest of the output doesn't change.

Consider these two new components representing `Logout` and `Login` buttons:

Login.js
```js
function Login(props) {
  return (
    <button onClick={props.onClick}>Login</button>
  )
}
```

Logout.js
```js
function Logout(props) {
  return (
    <button onClick={props.onClick}>Logout</button>
  )
}
```

in the example below we will create `stateful component` called `LoginControl`

LoginControl.js (Class)
```js
import React, { useState } from 'react'
import Login from './Login'
import Logout from './Logout'
import Greeting from './Greeting'

class LoginControl extends Component {
  constructor(props) {
    super(props);
    
    this.state = {
      isLoggedIn: false;
    }
    
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
  }
  
  handleLoginClick() {
    this.setState({ isLoggedIn: true })
  }
  
  handleLogoutClick() {
    this.setState({ isLoggedIn: false })
  }
  
  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {
      button = <Logout onClick={this.handleLogoutClick} />
    } else {
      button = <Login onClick={this.handleLoginClick} />
    }
    
    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    )
  }
}
```


## Inline if with Logical && Operator

```js
function Main(props) {
  const { unreadMessages } = props;
  
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 && 
        <h2>
          You have {unreadMessages.length} unread messages!
        </h2>
      }
    </div>
  )
}
```


## Inline if else with conditional operator

Another method for conditionally rendering elements inline is to use the JavaScript conditional operator `condition ? true : false`.

```js
render() {
  const isLoggedIn = this.state.isLoggedIn;
  
  return (  
    <h2>User is {isLoggedIn ? 'currently' : 'not'} logged in</h2>
  )
}
```

```js
render() {
  const isLoggedIn = this.state.isLoggedIn;
  
  return (
    <div>
      {isLoggedIn ?
        <Logout /> :
        <Login />
      }
    </div>
  )
}
```


## Preventing Component from Rendering

In rare cases you might want a component to hide itself even though it was rendered by another component. To do this return null instead of its render output.

In the example below, the `<WarningBanner />` is rendered depending on the value of the prop called warn. If the value of the prop is false, then the component does not render:

```js
function WarningBanner(props) {
  const warn = props.warn;
  
  if (!warn) {
    return null
  }
  
  return (
    <div>
      Warning!
    </div>
  )
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    
    this.state = {
      showWarning: false;
    }
    
    this.handleToggleWarning = this.handleToggleWarning.bind(this);
  }
  
  handleToggleWarning() {
    this.setState((state) => ({
      showWarning: !state.showWarning
    }))
  }
  
  render() {
    const showWarning = this.state.showWarning;
    
    return (
      <div>
        <WarningBanner warn={showWarning} />
        <button onClick={this.handleToggleWarning}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    )
  }
}
```
