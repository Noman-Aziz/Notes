# Introduction

### Introduction

* Environment to run javascript outside browser
* Built on Chrome's V8 JS engine
* Full Stack



### Browser JS vs Node JS

| Browser          | Node.Js          |
| ---------------- | ---------------- |
| DOM              | No DOM           |
| Window           | No Window        |
| Interactive Apps | Server Side Apps |
| No Filesystem    | Filesystem       |
| Fragmentation    | Versions         |
| ES6 Modules      | CommonJS         |



### Globals

| Keyword      | Action                                             |
| ------------ | -------------------------------------------------- |
| \_\_dirname  | path to current directory                          |
| \_\_filename | file name                                          |
| require      | function to use modules (CommonJs)                 |
| module       | info about current module (file)                   |
| process      | info about env where the program is being executed |



### Modules

* Encapsulated Code, Only share mininum
* Exported using `module.exports`
* Imported using `require()`

#### Built-in Modules

* OS
* PATH
* FS
* HTTP

#### Nodemon

* Installed as a global package usually
* Automatically restarts the app when modifying the code
* Included in `package.json` scripts as `nodemon app.js`



### Global Package vs NPX

* We should avoid installing dependencies globally since they can cause issues
* We should use NPX (Node Package Runner) to run packages without having to install them locally or globally



### package-lock.json

* When we install a node package of certain version, it also have its own dependencies of specific version
* this file contains the versions of the additional dependencies of the installed packages



### Package versioning (a.b.c)

* Whenever **a** changes, it means a major change (breaking change)
* **b** change is a minor change, it is backward compatible
* **c** change is a patch or bug fix

