# simple-git-promise  [![npm version](https://badge.fury.io/js/simple-git-promise.svg)](https://badge.fury.io/js/simple-git-promise)

**DEPRECATED:** This is just a 1-line wrapper around [`cmd-executor`](https://github.com/renolc/cmd-executor). You should probably just use that instead.

### Installation

```bash
npm i simple-git-promise -S
```

### Usage

```js
const git = require('simple-git-promise')
 
// All calls return a promise, so you should probably wait for them to complete 
// before running another command. You could use `.then()` or `await` 
;(async () => {
 
  // There are no specific attributes or functions defined on `git`. 
  // Instead, it is a proxy object that will take all attributes/function calls and 
  // parse them into a git command. For example: 
 
  // will run `git init` 
  await git.init()
 
  // will run `git add .` 
  await git.add('.')
 
  // will run `git commit -m "initial commit"` 
  await git.commit('-m "initial commit"')
 
  // will run `git remote add origin git@github.com:renolc/simple-git-promise.git` 
  await git.remote.add('origin', 'git@github.com:renolc/simple-git-promise.git')
 
  // Text that would be output by the git CLI are resolved by the promise 
  await git.branch('newBranch')
  const msg = await git.checkout('newBranch')
  console.log(msg) // "Switched to branch 'newBranch'\n" 
 
  // Finally, since what you can call on `git` is unbound, you could 
  // certainly do something nonsensical like: 
  try {
    await git.bork.blarg(42) // will try to run `git bork blarg 42` 
  } catch (e) {
    console.log(e) // error message containing "git: 'bork' is not a git command. See 'git --help'" 
  }
 
})()
```
