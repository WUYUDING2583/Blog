# fs.access(path[,mode],callback)

To check the user's permission for the file or directory specified by **path**.

**mode** specifies the accessibility check should be performed. Mode value should be `fs.constants.F_OK` for file exist check, `fs.constants.R_OK` for file readable check, `fs.constants.W_OK` file writable check.

**callback** is a function  invoked with a possible `Error` object, when the check is failed will pass an `Error` object, otherwise will pass `undefined` as parameter. The callback function will be invoked in **asynchronous**.

```js
import { access, constants } from 'node:fs';

const file = 'package.json';

// Check if the file exists in the current directory.
access(file, constants.F_OK, (err) => {
  console.log(`${file} ${err ? 'does not exist' : 'exists'}`);
});

// Check if the file is readable.
access(file, constants.R_OK, (err) => {
  console.log(`${file} ${err ? 'is not readable' : 'is readable'}`);
});

// Check if the file is writable.
access(file, constants.W_OK, (err) => {
  console.log(`${file} ${err ? 'is not writable' : 'is writable'}`);
});

// Check if the file is readable and writable.
access(file, constants.R_OK | constants.W_OK, (err) => {
  console.log(`${file} ${err ? 'is not' : 'is'} readable and writable`);
});
```

# fs.accessSync(path[,mode])

Check the accessibility of file synchronously, the parameters are same as with **fs.access**.

If the check fails, it will throw an error, otherwise it will return `undefined`.

```js
import { accessSync, constants } from 'node:fs';

try {
  accessSync('etc/passwd', constants.R_OK | constants.W_OK);
  console.log('can read/write');
} catch (err) {
  console.error('no access!');
}
```

