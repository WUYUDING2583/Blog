# path.resolve([...paths])

> Added in: v0.3.4

It receives a sequence of paths or path segments and converts them into an **absolute path**.

> Absolute path: a path starts with `/`
>

The given sequence of paths will be proceed from right to left, with each path prepended until an **absolute path** generated.

After all paths proceed, if an absolute path still haven't be generated, then the current working directory path will be prepended to it.

If the parameters are not provided, then `path.resolve()` will return the absolute path of current working directory.

```js
path.resolve('/foo/bar', './baz');
// Returns: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// Returns: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// If the current working directory is /home/myself/node,
// this returns '/home/myself/node/wwwroot/static_files/gif/image.gif'
```

