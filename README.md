# React-Conditional-Rendering

in `React` you can create `distinct` components that encapsulate behaviour you need. Then you can render only some of them. depending on the `state` of your application.

Consider these two components:

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
