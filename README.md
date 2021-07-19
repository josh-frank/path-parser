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

Takes a text path as an argument and parses it to a `Path` objects:

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

Returns the path as a string; path arguments are joined with spaces. Add/omit a relative flag `true` to return an absolute/relative path.

### `Path.adjustPoint( index, absoluteX, relativeX )`

Moves the point at a particular `index` to the coordinate `[ absoluteX, absoluteY ]`.

### `Path.adjustStartHandlePoint( index, absoluteX, relativeX )`

If the point at a particular `index` is a curve with a `startHandle`, moves `startHandle` to the coordinate `[ absoluteX, absoluteY ]`. Does nothing if the point at `index` is not a `c`ubic or `q`uadratic curve.

### `Path.adjustEndHandlePoint( index, absoluteX, relativeX )`

If the point at a particular `index` is a `c`ubic curve with an `endHandle`, moves `endHandle` to the coordinate `[ absoluteX, absoluteY ]`. Does nothing if the point at `index` is not a `c`ubic curve.

### `Path.snapToGrid( gridInterval )`

Rounds all points in `Path` to `gridInterval` ('snapping' the `Path`'s points to the `gridInterval`).

### `Path.translate( relativeX, relativeY )`

Translates all points in `Path` by `[ relativeX, relativeY ]`.

### `Path.scale( scaleX, scaleY )`

Scales `Path` by the ratio `[ scaleX, scaleY ]`.
