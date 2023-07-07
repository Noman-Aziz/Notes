# Jest js

### Writing test cases

* Written in files with extension `.test.js`
* Can be setup in `package.json` script `test: jest --watchAll --verbose`
  * `--watchAll` allows our code to be watched in the background and re run the tests when changes

```js
class Stack {
	constructor() {
		this.top = -1;
		this.items = {};
	}

	get peek() {
		return this.items[this.top];
	}

	push(value) {
		this.top += 1;
		this.items[this.top] = value;
	}

	pop() {
		this.top -= 1;
	}
}

// describe is used to define test suite

describe('My Stack', () => {
	let stack;

	// jest has helper functions like beforeEach, afterEach, beforeAll, afterAll
	beforeEach(() => {
		stack = new Stack();
	});

	// test/it function used for defining individual tests
	it('is created empty', () => {
		// toBe is a matcher which is used to match actual value with expected value
		expect(stack.top).toBe(-1);

		// toEqual matcher checks for value equality instead of object reference itself
		expect(stack.items).toEqual({});
	});

	it('can push to the top', () => {
		stack.push(2)

		expect(stack.top).toBe(0)
		expect(stack.peek).toBe(2)
	});


	// it.todo used to pass test while you fix the issues
	it('can pop off', () => {
		stack.push(2)
		stack.push(3)

		expect(stack.top).toBe(1)
		expect(stack.peek).toBe(3)

		stack.pop()

		expect(stack.top).toBe(0)
		expect(stack.peek).toBe(2)
	});
})
```



### Code Coverage

* Tells us how much our tests cover our source code
* We can add `--coverage` option in our `package.json` jest script section



### End-to-End Testing

* Done in jest by using the `jest-puppeteer` package

