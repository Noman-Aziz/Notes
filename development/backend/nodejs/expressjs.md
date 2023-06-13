# ExpressJs

### Basic Setup

```js
const express = require('express')
const app = express()

// Setup static and middleware
app.use(express.static('./public'))

app.get('/', (req, res) => {
	res.send('Home Page')
})

app.all('*', (req, res) => {
	res.status(404).send('<h1>Page not found</h1>')
})

app.listen(5000, () => {
	console.log('Server is listening on port 5000...')
})
```

***

### API vs SSR

| API        | SSR           |
| ---------- | ------------- |
| JSON       | Template      |
| Send Data  | Send Template |
| Res.JSON() | Res.Render()  |

***

### JSON APIs

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
	res.json([
			{ name: "john" },
			{ name: "joe" }
		])
})

app.listen(5000, () => {
	console.log("Server is listening on port 5000...")
})
```

***

### Middlewares

* These are functions that gets executed during the request to the server
* Has access to request and response object
* We must pass on the request to next middleware

#### Method 1

```js
const express = require('express')
const app = express()

const logger = (req, res, next) => {
	const method = req.method
	const url = req.url
	const time = new Date().getFullYear()
	console.log(method, url, time)
	next() // Sending back to Home Page
}

app.get('/', logger, (req, res) => {
	res.send("Home")
})

app.listen(5000, () => {
	console.log("Server is listening on port 5000...")
})
```

#### Method 2

**middleware.js**

```js
const logger = (req, res, next) => {
	const method = req.method
	const url = req.url
	const time = new Date().getFullYear()
	console.log(method, url, time)
	next() // Sending back to Home Page
}

module.exports = logger
```

**app.js**

```js
const express = require('express')
const app = express()
const logger = require('./middleware')

app.use(logger)

app.get('/', (req, res) => {
	res.send("Home")
})

app.get('/about', (req, res) => {
	res.send("About")
})

app.listen(5000, () => {
	console.log("Server is listening on port 5000...")
})
```

#### Types

1. Own
2. Express
3. Third Party
   1. Morgan (Logger)

***

### POST Method

```js
// parse form data
app.use(express.urlencoded({ extended: false }))

// parse json data
// app.use(express.json())

app.post('/login', (req, res) => {
	const { name } = req.body

	if(name) {
		return res.status(200).send(`Welcome ${name}`)
	}

	res.status(401).send('Please provide credentials!')
})
```

***

### Express Router

#### people.js

```js
const express = require('express')
const router = express.Router()

router.get('/', (req, res) => {
	res.send("P1, P2, P3")
})

router.post('/', (req, res) => {
	res.send("P1, P2, P3, P4")
})

router.get('/single', (req, res) => {
	res.send("P1")
})

module.exports = router
```

#### auth.js

```js
const express = require('express')
const router = express.Router()

router.post('/', (req, res) => {
	const { name } = req.body

	if(name) {
		return res.status(200).send(`Welcome ${name}`)
	}

	res.status(401).send('Please provide credentials!')
})

module.exports = router
```

#### app.js

```js
const people = require('./people')
const auth = require('./auth')

app.use(express.urlencoded({ extended: false }))
app.use(express.json())

app.use('/api/people', people)
app.use('/login', auth)
```

***

### Express Router Controllers (MVC)

#### people.js

```js
const getPeople = (req, res) => {
	res.send("P1, P2, P3")
}

const postPeople = (req, res) => {
	res.send("P1, P2, P3, P4")
}

const getSingle = (req, res) => {
	res.send("P1")
})

module.exports = {
	getPeople,
	postPeople,
	getSingle
}
```

#### people-router.js

```js
const {
	getPeople,
	postPeople,
	getSingle
} = require('./people.js')

// router.get('/', getPeople)
// router.post('/', postPeople)
// router.get('/single', getSingle)

router.route('/').get(getPeople).post(postPeople)
router.route('/single').get(getSingle)
```

***

### Mongoose

* Mongodb object modelling library for node.js

***
