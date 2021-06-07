# `path-parser`

`path-parser` is a tool for parsing SVG paths to objects with mutable commands and viewbox coordinates.

## `PathParser` methods

### `PathParser.parseRaw( path )`

## `Path` methods

### `new Path( descriptor )`
### `Path.toString( relative )`
### `Path.parse( definition )`
### `Path.adjustPoint( index, absoluteX, relativeX )`
### `Path.adjustStartHandlePoint( index, absoluteX, relativeX )`
### `Path.adjustEndHandlePoint( index, absoluteX, relativeX )`
### `Path.snapToGrid( gridInterval )`
### `Path.translate( relativeX, relativeY )`
