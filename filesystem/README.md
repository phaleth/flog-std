*This is API is partially implemented and not ready yet.*

# Filesystem API

```js
import {File} from "std/filesystem";

// reads the file `input.text` in the current directory into `file`
const file = await File.read("input.text");
```

## Spec

*Pseudo-Types reused in later definitions.*

```
type PathArgument = string | Path | File;
```

### Path

Representation of a filesystem path.

#### constructor(...args: PathArgument[]): Path

Creates a new object. Lazily holds a reference to the file and doesn't perform
any IO operations (or check that the file even exists).

#### #join(...paths: PathArgument[]): Path

Returns a new path with the given paths appended to current object's path;

```js
new Path("/home/flog").path === new Path("/home").join("flog").path;
```

#### get #directory: Path
Returns a new path with the directory part of the current object's path as
its path.

```js
new Path("/home/flog").directory.path === new Path("/home").path;
```

#### get #name: String
Returns the filename part of the current object's path with its extension.

```js
new Path("/home/flog/file.txt").name === "file.txt";
```

#### get #base: String
Returns the filename part of the current object's path without its extension.

```js
new Path("/home/flog/file.txt").base === "file";
```

#### get #extension: String
Returns the filename extension part of the current object's path.

```js
new Path("/home/flog/file.txt").extension === "txt";
```

#### #is(pattern: RegExp): boolean
Returns whether the current object's path fulfills the given pattern.

#### Path.is(path: PathArgument, pattern: RegExp)
Alias for `new Path(path).is(pattern)`;

#### Path.resolve(...paths: string[]): Path
Returns a new path using the resolved paths.

### `File`

Representation of a file object (this can be a file, a directory, a symlink,
etc.).

### License

AGPL3.0