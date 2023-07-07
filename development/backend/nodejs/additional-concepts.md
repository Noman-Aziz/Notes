# Additional Concepts

### Event Loops

* It is what allows Node.js to perform non-blocking I/O operations
  * Despite the fact that Javascript is single threaded
  * By offloading operations to the system kernel whenever possible
* It looks into the **task queue** and whenever **call stack** is empty, it pops the task from task queue and pushes it in call stack
* [https://www.youtube.com/watch?v=8aGhZQkoFbQ](https://www.youtube.com/watch?v=8aGhZQkoFbQ) (browser)
* [https://www.youtube.com/watch?v=PNa9OMajw9w](https://www.youtube.com/watch?v=PNa9OMajw9w) (backend)

#### Example

```js
console.log('first')
setTimeout(() => {
	console.log('second')
}, 0)
console.log('third')

// OUTPUTS
// first
// third
// second
```



### Promises

```js
const { readFile } = require('fs')

const getText = (path) = {
	return new Promise((resolve, reject) => {
		readFile(path, 'utf8', (err, data) => {
			if (err) {
				reject(err)
			} else {
				resolve(data)
			}
		})
	})
}

getText('./file.txt')
	.then((result) => console.log(result))
	.catch((err) => console.log(err))
```



### Async/Await

#### Method 1

```js
const start = async() => {
	try{
		const first = await getText('./file.txt')
		console.log(first)
	} catch (error) {
		console.log(error)
	}
}

start()
```

#### Method 2

```js
const { readFile } = require('fs')
const util = require('util')

const readFilePromise = util.promisify(readFile)

const start = async() => {
	try{
		const first = await readFilePromise('./file.txt', 'utf8')
		console.log(first)
	} catch (error) {
		console.log(error)
	}
}

start()
```

#### Method 3

```js
const { readFile } = require('fs').promises

const start = async() => {
	try{
		const first = await readFile('./file.txt', 'utf8')
		console.log(first)
	} catch (error) {
		console.log(error)
	}
}

start()
```



### Events

* Event Driven Programming is used heavily in NodeJS

#### Example 1

```js
const EventEmitter = require('events')

const customEmitter = new EventEmitter()

customEmitter.on('response', () => {
	console.log(`data received`)
})

customEmitter.emit('response')
```

#### Example 2

```js
const http = require('http')

const server = http.createServer()

server.on('request', (req, res) => {
	res.end('Welcome')
})

server.listen(5000)
```



### Streams

* Extends EventEmitter class
* As file gets bigger and bigger, we should not read the whole file and store it in a variable

#### Types

* Writeable
* Readable
* Duplex
  * Used to both read and write data sequentially
* Transform
  * Data can be modified while writing or reading

#### Example 1

**Write.js**

```js
const { writeFileSync } = require('fs')

for (let i=0; i < 10000 ; i++) {
	writeFileSync('./file.txt', `hello world ${i}\n`, { flag: 'a' })
}
```

**Reading.js**

```js
const { createReadStream } = require('fs')

// Reading data in chunks of 90kb, default is 64kb
const stream = createReadStream('./file.txt', {
	highWaterMark: 90000,
	encoding: 'utf8'
});

stream.on('data', (result) => {
	console.log(result)
})

stream.on('error', (error) => {
	console.log(error)
})
```

#### Example 2

```js
var http = require('http')
var fs = require('fs')

http.createServer(function (req, res) {
	// Sending Data at Once
	// const text = fs.readFileSync('./file.txt', 'utf8')
	// res.end(text)
	
	// Sending Data in Chunks
	const fileStream = fs.createReadStream('./file.txt', 'utf8');
	
	fileStream.on('open', () => {
		fileStream.pipe(res)
	})
	
	fileStream.on('error', (err) => {
		res.end(err)
	})
})
```

