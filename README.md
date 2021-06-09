# `path-parser`

`path-parser` is a tool for parsing SVG paths to objects with mutable commands and viewbox coordinates. It represents a `Path` as a doubly-linked list of `PathCommand` nodes.

## `PathParser`

`PathParser` is essentially a static class and it has only one public method.

### `PathParser.parseRaw( path )`
Takes a text path as an argument and parses to an array-of-arrays containing primitives:

```
PathParser.parseRaw( "m 744 136 h -202 c -10 0 -18 8 -18 18 h 238 c 0 -10 -8 -18 -18 -18 z" )

> [
    [ 'm', 744, 136 ],
    [ 'h', -202 ],
    [ 'c', -10, 0,  -18, 8, -18, 18 ],
    [ 'h', 238 ],
    [ 'c', 0, -10, -8, -18, -18, -18 ],
    [ 'z' ]
  ]
```

`parseRaw()` throws an `Error()` when it encounters an invalid path so it's easy to validate a path with `try {} catch {}`.

## `Path`

### `new Path( descriptor )`
Takes a text path as an argument and parses it an array of `PathCommand` objects:

```
const testPath = new Path( "m 744 136 h -202 c -10 0 -18 8 -18 18 h 238 c 0 -10 -8 -18 -18 -18 z" )

> Path {
  definition: 'm 744 136 h -202 c -10 0 -18 8 -18 18 h 238 c 0 -10 -8 -18 -18 -18 z',
  parsedCommands: [
    PathCommand {
      index: 0,
      commandLetter: 'm',
      absolutePrevious: [Array],
      absoluteNext: [Array],
      absoluteCommand: [Array],
      relativeCommand: [Array],
      next: [PathCommand]
    }
    ...<4 more>
  ]
}
```

### `Path.toString( relative )`
### `Path.adjustPoint( index, absoluteX, relativeX )`
### `Path.adjustStartHandlePoint( index, absoluteX, relativeX )`
### `Path.adjustEndHandlePoint( index, absoluteX, relativeX )`
### `Path.snapToGrid( gridInterval )`
### `Path.translate( relativeX, relativeY )`
### `Path.scale( scaleX, scaleY )`
