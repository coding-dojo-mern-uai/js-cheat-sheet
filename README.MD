# Fundamentals

### Scopes
```js

// Global scope
const text = "this is a string"
let number = 0

// Local scope
const hook = () => {

}
// Local scope
const func = () => {
  // Global scope de postSum
  const inc = 1
  hook()
  // Local scope
  const postSum = () => {
    const postVariable = 0
    hook()
    func()
  }
  return number + inc  
}
```
### Destructuring
```js
const person = {
  firstName: 'Bob',
  lastName: 'Marley',
  email: 'bob@marley.com',
  password: 'sekureP@ssw0rd9',
  username: 'barley',
  addresses: [
    {
      address: '1600 Pennsylvania Avenue',
      city: 'Washington, D.C.',
      zipcode: '20500',
    },
    {
      address: '221B Baker St.',
      city: 'London',
      zipcode: 'WC2N 5DU',
    }
  ],
  createdAt: 1543945177623
};

// const email = person.email
const {email} = person

// const mail = person.email
const {email: mail} = person
// const firstAddress = person.addresses[0].city
const {addresses : [{city}]} = person
// const email = person.email
// const addresses = person.addresses
// const username = person.username
const {email, addresses, username} = person

const animals = ['horse', 'dog', 'fish', 'cat', 'bird'];
// const firstAnimal = animals[0]
// const restOfAnimals = animals.slice(1)
const [firstAnimal, ...restOfAnimals] = animals;
```
### Spread
```js
// Resize a variable
const { firstName, lastName, ...attributes } = person;
const [firstAnimal, ...restOfAnimals] = animals;

// Copy objects or arrays
const personCopy = {...person}
// Merge two objects
{...user, ...currentAttr}
const animalsCopy = [...animals]
// Merge two arrays
[...user, ...currentAttr]
```

### Array
```js
const obj = {}
// This wont work
obj.map()

const arr = []
// Arr Size
arr.length
// return array
arr.map(el => func())
// return array
arr.filter(el => condition())
// return var
arr.find(el => condition())
// execute functions
arr.forEach(el => func())
// insert data inside an array
arr.push(el)
```
### Obj
```js
let personArray = []
const person = {
  firstName: 'Bob',
  lastName: 'Marley',
  email: 'bob@marley.com',
  password: 'sekureP@ssw0rd9',
  username: 'barley',
  addresses: [
    {
      address: '1600 Pennsylvania Avenue',
      city: 'Washington, D.C.',
      zipcode: '20500',
    },
    {
      address: '221B Baker St.',
      city: 'London',
      zipcode: 'WC2N 5DU',
    }
  ],
  createdAt: 1543945177623
};


// [['firstName', ..., 'createdAt'], ['Bob', ..., 1543945177623]]
const entries = Object.entries(person)
// ['firstName', ..., 'createdAt']
const keys = Object.keys(person)
// ['Bob', ..., 1543945177623]
const values = Object.values(person)

// Declarativa
person.email // get value
{email: "test@test.com"} // set key
// Programatica
person["email"] // get value
{[email]: "test@test.com"} // set key
keys.map(key => personArray.push({[key]: person[key]}))
```

### Async / await
```js

const asyncFunc = async () => {
  const query = await find()
  const insert = await insert()
}

const inlineAsyncFunc = () => find()
  
const func = async function() => {
  await asyncFunc()
  await inlineAsyncFunc()
}

```

# React

### Basic
```js
// Import react always
import React, {useEffect} from 'react'

// Components names always start with Uppercase
const Comp = (props) => {
  return <span />
}

// Export component
export default Comp
```

### Component Lifecycle
```js
// Import react always
import React, {useEffect, useState} from 'react'

const Comp = (props) => {
  const [state, setState] = useState()
  // componentDidMount
  useEffect(() => {}, [])
  // componentDidUpdate or shouldComponentUpdate
  // Cannot use setState
  useEffect(() => {}, [state])
  // componentWillUnmount
  useEffect(() => {
    return () => {}
  }, [])
  
  return <span />
}

// Export component
export default Comp
```

### Props & States
```js
import React, { useState } from 'react'

export const ChildComponent = ({color, changeColor}) => {
  // state = current state value
  // setState = func modify state
  // useState(defaultValue)
  const [state, setState] = useState()
  useEffect(()=> changeColor(), [])
  return <span />
}

export const ParentComponent = (props) => {
  return 
    <ChildComponent 
      color="red" 
      size={10} 
      changeColor={() => setColor()}
      style={{backgroundColor: 'red'}}
    />
}

// App.js
import {CompA, CompB} from ...

```
### Synthetic Events

```js
import React, { useState } from 'react'

const Comp = (props) => {

const [user, setUser] = useState({})

const changeInputHandler = ({target: {name, value}}) => {
  // {username: ro} 
  const currentAttr = {[name]: value}
  // {username: r, {username: ro}}
  //setUser({...user, currentAttr})
  //setUser({...user, {[name]: value}})
  setUser({...user, ...currentAttr})
}

// const changeInputHandler = ({target: {name, value}}) =>  setUser({...user, ...currentAttr})
  
  return 
    <input
      name="username"
      onChange={changeInputHandler}
      onBlur
      onSubmit
      onKeyDown 
      onKeyPress 
      onKeyUp
      onFocus
      onClick
      onDoubleClick
      onScroll
    />
    <input
      name="username"
      onChange={changeInputHandler}
    />
}

// Export component
export default Comp
```

### React Router
```
npm install react-router-dom --save
```

```js
// index.js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
import reportWebVitals from './reportWebVitals'

import { BrowserRouter } from 'react-router-dom'


ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter> //---> Remember add this context
      <App />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root')
)

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals()

//App.js
import { Switch, Route } from 'react-router-dom'

import UpdateJoke from './pages/UpdateJoke'
// _id es un prop de UpdateJoke
// title es un parametro opcional
function App() {
  return (
    <div>
        <Switch>
          {/* http://localhost:3000/jokes/:_id/edit */}
          <Route exact path="/jokes/create" component={UpdateJoke} />
          <Route exact path="/jokes/:_id/edit" component={UpdateJoke} />
          <Route exact path="/jokes/:_id/(:title)/edit" component={UpdateJoke} />
        </Switch>

    </div>
  )
}
export default App
```
### React Router History & Params
```js

import React, {useEffect} from 'react'
import {useParams, useHistory} from 'react-router-dom'


const Comp = (props) => {
  const {_id, title} = useParams()
  const history = useHistory()
  // history.push()
  return <span />
}

// Export component
export default Comp
```

### Commands
``` bash
# Init react
npx create-react-app [app-name]
# Install packages from npm package
npm install
# Run react code
npm start 
# Compile react code
npm run build
# Install and save local package
npm install express --save

```

# Express

### Commands
``` bash
# Init node project
npm init
# Install packages from npm package
npm install
# Install and save local package
npm install express --save
# Install and save global package
npm install nondemon -g
# Run node code
npm start index.js
# Run custom script
npm run start:dev
```

### Structure
**Routes:** Rutas de la aplicación.
**Controllers:** req, res y ejecutan services.
**Services:** Interactuan con la db, interactuan con otras librerías y ejecutan código.
**Middlewares:** Validan si se puede resolver una petición.
**Config:** Configuración del proyecto.

### Express Routing

```js
// routes/users.js
const { Router } = require('express')
const {UsersController} = require('../controllers/UsersController')

// id es un parametro
const router = Router()

router.get("/users/:id", UsersController.getUser)
router.post("/users/:id", UsersController.editUser)
// UsersController.js
module.exports = {
  getUser:  (req, res) => {
    console.log(req.params.id)
    // si no usamos res nuestra cae en un loop infinito
    res.json( users[req.params.id] )
  },
  editUser(req, res) => {
    console.log(req.body)
    res.json( users[req.params.id] )
  }
}
```
### Express middleware
```js
// routes/users.js
router.get("/users/:id", autenticate, UsersController.getUser)

// config/auth.js
const { verifyUserId } = require('../services/auth.service')

module.exports = {
  authenticate: async (req, res, next) => {
    try {
      const { authToken } = req.cookies
      const userId = verifyUserId(authToken)
      req.userId = userId
      next()
    } catch (error) {
      res.status(401).send('Unauthorized')
    }
  }
```
### Mongo Functions
```js
const findUser = async (query) => await User.findOne(query)

const insertUser = async (data) => {
  const user = new User(data)
  await user.save()
}

const updateUser = async() => {
  // new: true, return updated doc
  // runValidators: true, validate data before update
  await User.findOneAndUpdate({query}, {data}, { new: true, runValidators: true })
}

const deleteUser = async () => await User.deleteOne({query})

```
### Mongoose Models

```js
const Mongoose = require('mongoose')
// install bcrypt
const bcrypt = require('bcrypt')

const UserSchema = new Mongoose.Schema(
  {
    email: { type: String, unique: true },
    password: { type: String }
  },
  // fechas por defecto
  { timestamp: true }
)

// Campos que solo usamos en el codigo pero no que van a la db
UserSchema.virtual('confirmPassword')

// Ejecuta una función antes de validar
UserSchema.pre('validate', function (next) {
  if (this.password !== this.confirmPassword) this.invalidate('confirmPassword', 'Passwords dont match')
  next()
})

// PRE: Save, callback
UserSchema.pre('save', async function (next) {
  try {
    const hash = await bcrypt.hash(this.password, 10)
    this.password = hash
    next()
  } catch (error) {
    next()
  }
})

module.exports = Mongoose.model('User', UserSchema)

```

### Auth

```js
// Método de encriptación entre el servidor y el cliente
// npm install jsonwebtoken --save
const jwt = require("jsonwebtoken")

const secretKey = "codingdojo"

const payload = {
  _id: user._id
}

const myJWT = jwt.sign(payload, secretKey)
const decryptedPayload = jwt.verify(token, secretKey)
```

### Cookies
```js
const cookieParser = require('cookie-parser');
app.use(cookieParser());
// Change the app.use(cors()) to the one below
app.use(cors({credentials: true, origin: 'http://localhost:3000'}));

res
  .cookie("mycookie", "mydata", { httpOnly: true })
  .json({ message: "This response has a cookie" });
```


# Sockets

### Server
```js
const express = require('express')
const socketIO = require('socket.io')

const server = app.listen(8080, () => console.log('server running'))
const io = socketIO(server, { cors: true })

io.on('connection', (socket) => {
  // Creación de canales especificos
  socket.join(room)

  // listen events
  socket.on('new-data', (data) => {
    // Emitiendo dentro de un canal
    io.in(room).emit('new-data', {data})
    // Emitir data por meido del socket
    io.emit('new-data', {data})
  })

  // Salir del socket
  socket.on('disconnect', () => {
    socket.leave(room)
  })
})

```

### Client
```js
import React, { useEffect, useState } from 'react'
import socketIOClient from 'socket.io-client'

const PingButton = () => {
  const [socketClient, setSocketClient] = useState()
  const [message, setMessage] = useState()
  const [messages, setMessages] = useState()

  //Escuchar un evento o canal, GET
  useEffect(() => {
    const socket = socketIOClient('http://localhost:8001')
    socket.on('new-data', (data) => setMessages(data))
    setSocketClient(socket)
    return () => socket.disconnect(true)
    //
  }, [])
  
  //Emitir un evento, POST
  const onClickHandler = () => {
    socketClient.emit('new-data', {
      body: message,
      senderId: socketClient.id
    })
  }

  return (
    <div>
      <h1>Ping Button</h1>
      <p>Message</p>

      {messages &&
        messages.map((message, key) => (
          <p key={key}>
            {message.senderId}: {message.body}
          </p>
        ))}
      <input type="text" name="message" onChange={(e) => setMessage(e.target.value)} />
      <button onClick={onClickHandler}>Send</button>
    </div>
  )
}

export default PingButton
```

# Git
### Commands
``` bash
# Inicializar git en nuestra carpeta
git init
```
