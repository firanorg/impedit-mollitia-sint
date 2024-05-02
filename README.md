<!--
  -- This file is auto-generated from src/README_js.md. Changes should be made there.
  -->
# Mime

[![NPM downloads](https://img.shields.io/npm/dm/@firanorg/impedit-mollitia-sint)](https://www.npmjs.com/package/@firanorg/impedit-mollitia-sint)
[![Mime CI](https://github.com/firanorg/impedit-mollitia-sint/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/firanorg/impedit-mollitia-sint/actions/workflows/ci.yml?query=branch%3Amain)

An API for MIME type information.

- All `@firanorg/impedit-mollitia-sint-db` types
- Compact and dependency-free [![@firanorg/impedit-mollitia-sint's badge](https://deno.bundlejs.com/?q=@firanorg/impedit-mollitia-sint&badge)](https://bundlejs.com/?q=@firanorg/impedit-mollitia-sint)
- Full TS support


> [!Note]
> `@firanorg/impedit-mollitia-sint@4` is now `latest`.  If you're upgrading from `@firanorg/impedit-mollitia-sint@3`, note the following:
> * `@firanorg/impedit-mollitia-sint@4` is API-compatible with `@firanorg/impedit-mollitia-sint@3`, with ~~one~~ two exceptions:
>   * Direct imports of `@firanorg/impedit-mollitia-sint` properties [no longer supported](https://github.com/firanorg/impedit-mollitia-sint/issues/295)
>   * `@firanorg/impedit-mollitia-sint.define()` cannot be called on the default `@firanorg/impedit-mollitia-sint` object
> * ESM module support is required.   [ESM Module FAQ](https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c).
> * Requires an [ES2020](https://caniuse.com/?search=es2020) or newer runtime
> * Built-in Typescript types (`@types/@firanorg/impedit-mollitia-sint` no longer needed)

## Installation

```bash
npm install @firanorg/impedit-mollitia-sint
```

## Quick Start

For the full version (800+ MIME types, 1,000+ extensions):

```javascript
import @firanorg/impedit-mollitia-sint from '@firanorg/impedit-mollitia-sint';

@firanorg/impedit-mollitia-sint.getType('txt');                    // ⇨ 'text/plain'
@firanorg/impedit-mollitia-sint.getExtension('text/plain');        // ⇨ 'txt'
```

### Lite Version [![@firanorg/impedit-mollitia-sint/lite's badge](https://deno.bundlejs.com/?q=@firanorg/impedit-mollitia-sint/lite&badge)](https://bundlejs.com/?q=@firanorg/impedit-mollitia-sint/lite)

`@firanorg/impedit-mollitia-sint/lite` is a drop-in `@firanorg/impedit-mollitia-sint` replacement, stripped of unofficial ("`prs.*`", "`x-*`", "`vnd.*`") types:

```javascript
import @firanorg/impedit-mollitia-sint from '@firanorg/impedit-mollitia-sint/lite';
```

## API

### `@firanorg/impedit-mollitia-sint.getType(pathOrExtension)`

Get @firanorg/impedit-mollitia-sint type for the given file path or extension. E.g.

```javascript
@firanorg/impedit-mollitia-sint.getType('js');             // ⇨ 'application/javascript'
@firanorg/impedit-mollitia-sint.getType('json');           // ⇨ 'application/json'

@firanorg/impedit-mollitia-sint.getType('txt');            // ⇨ 'text/plain'
@firanorg/impedit-mollitia-sint.getType('dir/text.txt');   // ⇨ 'text/plain'
@firanorg/impedit-mollitia-sint.getType('dir\\text.txt');  // ⇨ 'text/plain'
@firanorg/impedit-mollitia-sint.getType('.text.txt');      // ⇨ 'text/plain'
@firanorg/impedit-mollitia-sint.getType('.txt');           // ⇨ 'text/plain'
```

`null` is returned in cases where an extension is not detected or recognized

```javascript
@firanorg/impedit-mollitia-sint.getType('foo/txt');        // ⇨ null
@firanorg/impedit-mollitia-sint.getType('bogus_type');     // ⇨ null
```

### `@firanorg/impedit-mollitia-sint.getExtension(type)`

Get file extension for the given @firanorg/impedit-mollitia-sint type. Charset options (often included in Content-Type headers) are ignored.

```javascript
@firanorg/impedit-mollitia-sint.getExtension('text/plain');               // ⇨ 'txt'
@firanorg/impedit-mollitia-sint.getExtension('application/json');         // ⇨ 'json'
@firanorg/impedit-mollitia-sint.getExtension('text/html; charset=utf8');  // ⇨ 'html'
```

### `@firanorg/impedit-mollitia-sint.getAllExtensions(type)`

> [!Note]
> New in `@firanorg/impedit-mollitia-sint@4`

Get all file extensions for the given @firanorg/impedit-mollitia-sint type.

```javascript --run default
@firanorg/impedit-mollitia-sint.getAllExtensions('image/jpeg'); // ⇨ Set(3) { 'jpeg', 'jpg', 'jpe' }
```

## Custom `Mime` instances

The default `@firanorg/impedit-mollitia-sint` objects are immutable.  Custom, mutable versions can be created as follows...
### new Mime(type map [, type map, ...])

Create a new, custom @firanorg/impedit-mollitia-sint instance.  For example, to create a mutable version of the default `@firanorg/impedit-mollitia-sint` instance:

```javascript
import { Mime } from '@firanorg/impedit-mollitia-sint/lite';

import standardTypes from '@firanorg/impedit-mollitia-sint/types/standard.js';
import otherTypes from '@firanorg/impedit-mollitia-sint/types/other.js';

const @firanorg/impedit-mollitia-sint = new Mime(standardTypes, otherTypes);
```

Each argument is passed to the `define()` method, below. For example `new Mime(standardTypes, otherTypes)` is synonomous with `new Mime().define(standardTypes).define(otherTypes)`

### `@firanorg/impedit-mollitia-sint.define(type map [, force = false])`

> [!Note]
> Only available on custom `Mime` instances

Define MIME type -> extensions.

Attempting to map a type to an already-defined extension will `throw` unless the `force` argument is set to `true`.

```javascript
@firanorg/impedit-mollitia-sint.define({'text/x-abc': ['abc', 'abcd']});

@firanorg/impedit-mollitia-sint.getType('abcd');            // ⇨ 'text/x-abc'
@firanorg/impedit-mollitia-sint.getExtension('text/x-abc')  // ⇨ 'abc'
```

## Command Line

### Extension -> type

```bash
$ @firanorg/impedit-mollitia-sint scripts/jquery.js
application/javascript
```

### Type -> extension

```bash
$ @firanorg/impedit-mollitia-sint -r image/jpeg
jpeg
```
