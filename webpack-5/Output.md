`output` configuration tells webpack how to write the complied file into disk. We can only have **one** `output` configuration while we can have multiple `entry` points.

# Usage

## Minimum requirement

The easiest way to use specify `output` property is to set it as an object and provide the `output.filename` to use for the output file.

```javascript
module.exports={
  output:{
    filename: 'bundle.js'
  }
}
```

## Multiple Entry Points

When we config more than a single `chunk` means with multiple entry points, we should use **substitutions** to ensure that each output file has a unique name.

```javascript
module.exports={
  entry{
  	app: './src/app.js',
  	search: './src/search.js'
	},
  output:{
    filename: '[name].js',
    path: __dirname + '/dist'
  }
}
```

