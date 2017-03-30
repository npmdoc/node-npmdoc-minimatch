# api documentation for  [minimatch (v3.0.3)](https://github.com/isaacs/minimatch#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-minimatch.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-minimatch) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-minimatch.svg)](https://travis-ci.org/npmdoc/node-npmdoc-minimatch)
#### a glob matcher in javascript

[![NPM](https://nodei.co/npm/minimatch.png?downloads=true)](https://www.npmjs.com/package/minimatch)

[![apidoc](https://npmdoc.github.io/node-npmdoc-minimatch/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-minimatch_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-minimatch/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-minimatch/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Isaac Z. Schlueter",
        "email": "i@izs.me",
        "url": "http://blog.izs.me"
    },
    "bugs": {
        "url": "https://github.com/isaacs/minimatch/issues"
    },
    "dependencies": {
        "brace-expansion": "^1.0.0"
    },
    "description": "a glob matcher in javascript",
    "devDependencies": {
        "standard": "^3.7.2",
        "tap": "^5.6.0"
    },
    "directories": {},
    "dist": {
        "shasum": "2a4e4090b96b2db06a9d7df01055a62a77c9b774",
        "tarball": "https://registry.npmjs.org/minimatch/-/minimatch-3.0.3.tgz"
    },
    "engines": {
        "node": "*"
    },
    "files": [
        "minimatch.js"
    ],
    "gitHead": "eed89491bd4a4e6bc463aac0dfb5c29ef0d1dc13",
    "homepage": "https://github.com/isaacs/minimatch#readme",
    "license": "ISC",
    "main": "minimatch.js",
    "maintainers": [
        {
            "name": "isaacs",
            "email": "i@izs.me"
        }
    ],
    "name": "minimatch",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/isaacs/minimatch.git"
    },
    "scripts": {
        "posttest": "standard minimatch.js test/*.js",
        "test": "tap test/*.js"
    },
    "version": "3.0.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module minimatch](#apidoc.module.minimatch)
1.  [function <span class="apidocSignatureSpan">minimatch.</span>Minimatch (pattern, options)](#apidoc.element.minimatch.Minimatch)
1.  [function <span class="apidocSignatureSpan">minimatch.</span>braceExpand (pattern, options)](#apidoc.element.minimatch.braceExpand)
1.  [function <span class="apidocSignatureSpan">minimatch.</span>defaults (def)](#apidoc.element.minimatch.defaults)
1.  [function <span class="apidocSignatureSpan">minimatch.</span>filter (pattern, options)](#apidoc.element.minimatch.filter)
1.  [function <span class="apidocSignatureSpan">minimatch.</span>makeRe (pattern, options)](#apidoc.element.minimatch.makeRe)
1.  [function <span class="apidocSignatureSpan">minimatch.</span>match (list, pattern, options)](#apidoc.element.minimatch.match)
1.  object <span class="apidocSignatureSpan">minimatch.</span>GLOBSTAR
1.  object <span class="apidocSignatureSpan">minimatch.</span>Minimatch.prototype

#### [module minimatch.Minimatch](#apidoc.module.minimatch.Minimatch)
1.  [function <span class="apidocSignatureSpan">minimatch.</span>Minimatch (pattern, options)](#apidoc.element.minimatch.Minimatch.Minimatch)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.</span>defaults (def)](#apidoc.element.minimatch.Minimatch.defaults)
1.  object <span class="apidocSignatureSpan">minimatch.Minimatch.</span>GLOBSTAR

#### [module minimatch.Minimatch.prototype](#apidoc.module.minimatch.Minimatch.prototype)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>braceExpand (pattern, options)](#apidoc.element.minimatch.Minimatch.prototype.braceExpand)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>debug ()](#apidoc.element.minimatch.Minimatch.prototype.debug)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>make ()](#apidoc.element.minimatch.Minimatch.prototype.make)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>makeRe ()](#apidoc.element.minimatch.Minimatch.prototype.makeRe)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>match (f, partial)](#apidoc.element.minimatch.Minimatch.prototype.match)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>matchOne (file, pattern, partial)](#apidoc.element.minimatch.Minimatch.prototype.matchOne)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>parse (pattern, isSub)](#apidoc.element.minimatch.Minimatch.prototype.parse)
1.  [function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>parseNegate ()](#apidoc.element.minimatch.Minimatch.prototype.parseNegate)



# <a name="apidoc.module.minimatch"></a>[module minimatch](#apidoc.module.minimatch)

#### <a name="apidoc.element.minimatch.Minimatch"></a>[function <span class="apidocSignatureSpan">minimatch.</span>Minimatch (pattern, options)](#apidoc.element.minimatch.Minimatch)
- description and source-code
```javascript
function Minimatch(pattern, options) {
  if (!(this instanceof Minimatch)) {
    return new Minimatch(pattern, options)
  }

  if (typeof pattern !== 'string') {
    throw new TypeError('glob pattern string required')
  }

  if (!options) options = {}
  pattern = pattern.trim()

  // windows support: need to use /, not \
  if (path.sep !== '/') {
    pattern = pattern.split(path.sep).join('/')
  }

  this.options = options
  this.set = []
  this.pattern = pattern
  this.regexp = null
  this.negate = false
  this.comment = false
  this.empty = false

  // make the set of regexps etc.
  this.make()
}
```
- example usage
```shell
...
var orig = minimatch

var m = function minimatch (p, pattern, options) {
  return orig.minimatch(p, pattern, ext(def, options))
}

m.Minimatch = function Minimatch (pattern, options) {
  return new orig.Minimatch(pattern, ext(def, options))
}

return m
}

Minimatch.defaults = function (def) {
if (!def || !Object.keys(def).length) return Minimatch
...
```

#### <a name="apidoc.element.minimatch.braceExpand"></a>[function <span class="apidocSignatureSpan">minimatch.</span>braceExpand (pattern, options)](#apidoc.element.minimatch.braceExpand)
- description and source-code
```javascript
braceExpand = function (pattern, options) {
  return braceExpand(pattern, options)
}
```
- example usage
```shell
...
  return
}

// step 1: figure out negation, etc.
this.parseNegate()

// step 2: expand braces
var set = this.globSet = this.braceExpand()

if (options.debug) this.debug = console.error

this.debug(this.pattern, set)

// step 3: now we have a set, so turn each one into a series of path-portion
// matching patterns.
...
```

#### <a name="apidoc.element.minimatch.defaults"></a>[function <span class="apidocSignatureSpan">minimatch.</span>defaults (def)](#apidoc.element.minimatch.defaults)
- description and source-code
```javascript
defaults = function (def) {
  if (!def || !Object.keys(def).length) return minimatch

  var orig = minimatch

  var m = function minimatch (p, pattern, options) {
    return orig.minimatch(p, pattern, ext(def, options))
  }

  m.Minimatch = function Minimatch (pattern, options) {
    return new orig.Minimatch(pattern, ext(def, options))
  }

  return m
}
```
- example usage
```shell
...
}

return m
}

Minimatch.defaults = function (def) {
if (!def || !Object.keys(def).length) return Minimatch
return minimatch.defaults(def).Minimatch
}

function minimatch (p, pattern, options) {
if (typeof pattern !== 'string') {
  throw new TypeError('glob pattern string required')
}
...
```

#### <a name="apidoc.element.minimatch.filter"></a>[function <span class="apidocSignatureSpan">minimatch.</span>filter (pattern, options)](#apidoc.element.minimatch.filter)
- description and source-code
```javascript
function filter(pattern, options) {
  options = options || {}
  return function (p, i, list) {
    return minimatch(p, pattern, options)
  }
}
```
- example usage
```shell
...

Main export.  Tests a path against the pattern using the options.

'''javascript
var isJS = minimatch(file, "*.js", { matchBase: true })
'''

### minimatch.filter(pattern, options)

Returns a function that tests its
supplied argument, suitable for use with 'Array.filter'.  Example:

'''javascript
var javascripts = fileList.filter(minimatch.filter("*.js", {matchBase: true}))
'''
...
```

#### <a name="apidoc.element.minimatch.makeRe"></a>[function <span class="apidocSignatureSpan">minimatch.</span>makeRe (pattern, options)](#apidoc.element.minimatch.makeRe)
- description and source-code
```javascript
makeRe = function (pattern, options) {
  return new Minimatch(pattern, options || {}).makeRe()
}
```
- example usage
```shell
...
files, in the style of fnmatch or glob.  If nothing is matched, and
options.nonull is set, then return a list containing the pattern itself.

'''javascript
var javascripts = minimatch.match(fileList, "*.js", {matchBase: true}))
'''

### minimatch.makeRe(pattern, options)

Make a regular expression object from the pattern.

## Options

All options are 'false' by default.
...
```

#### <a name="apidoc.element.minimatch.match"></a>[function <span class="apidocSignatureSpan">minimatch.</span>match (list, pattern, options)](#apidoc.element.minimatch.match)
- description and source-code
```javascript
match = function (list, pattern, options) {
  options = options || {}
  var mm = new Minimatch(pattern, options)
  list = list.filter(function (f) {
    return mm.match(f)
  })
  if (mm.options.nonull && !list.length) {
    list.push(pattern)
  }
  return list
}
```
- example usage
```shell
...
Returns a function that tests its
supplied argument, suitable for use with 'Array.filter'.  Example:

'''javascript
var javascripts = fileList.filter(minimatch.filter("*.js", {matchBase: true}))
'''

### minimatch.match(list, pattern, options)

Match against the list of
files, in the style of fnmatch or glob.  If nothing is matched, and
options.nonull is set, then return a list containing the pattern itself.

'''javascript
var javascripts = minimatch.match(fileList, "*.js", {matchBase: true}))
...
```



# <a name="apidoc.module.minimatch.Minimatch"></a>[module minimatch.Minimatch](#apidoc.module.minimatch.Minimatch)

#### <a name="apidoc.element.minimatch.Minimatch.Minimatch"></a>[function <span class="apidocSignatureSpan">minimatch.</span>Minimatch (pattern, options)](#apidoc.element.minimatch.Minimatch.Minimatch)
- description and source-code
```javascript
function Minimatch(pattern, options) {
  if (!(this instanceof Minimatch)) {
    return new Minimatch(pattern, options)
  }

  if (typeof pattern !== 'string') {
    throw new TypeError('glob pattern string required')
  }

  if (!options) options = {}
  pattern = pattern.trim()

  // windows support: need to use /, not \
  if (path.sep !== '/') {
    pattern = pattern.split(path.sep).join('/')
  }

  this.options = options
  this.set = []
  this.pattern = pattern
  this.regexp = null
  this.negate = false
  this.comment = false
  this.empty = false

  // make the set of regexps etc.
  this.make()
}
```
- example usage
```shell
...
var orig = minimatch

var m = function minimatch (p, pattern, options) {
  return orig.minimatch(p, pattern, ext(def, options))
}

m.Minimatch = function Minimatch (pattern, options) {
  return new orig.Minimatch(pattern, ext(def, options))
}

return m
}

Minimatch.defaults = function (def) {
if (!def || !Object.keys(def).length) return Minimatch
...
```

#### <a name="apidoc.element.minimatch.Minimatch.defaults"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.</span>defaults (def)](#apidoc.element.minimatch.Minimatch.defaults)
- description and source-code
```javascript
defaults = function (def) {
  if (!def || !Object.keys(def).length) return Minimatch
  return minimatch.defaults(def).Minimatch
}
```
- example usage
```shell
...
}

return m
}

Minimatch.defaults = function (def) {
if (!def || !Object.keys(def).length) return Minimatch
return minimatch.defaults(def).Minimatch
}

function minimatch (p, pattern, options) {
if (typeof pattern !== 'string') {
  throw new TypeError('glob pattern string required')
}
...
```



# <a name="apidoc.module.minimatch.Minimatch.prototype"></a>[module minimatch.Minimatch.prototype](#apidoc.module.minimatch.Minimatch.prototype)

#### <a name="apidoc.element.minimatch.Minimatch.prototype.braceExpand"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>braceExpand (pattern, options)](#apidoc.element.minimatch.Minimatch.prototype.braceExpand)
- description and source-code
```javascript
function braceExpand(pattern, options) {
  if (!options) {
    if (this instanceof Minimatch) {
      options = this.options
    } else {
      options = {}
    }
  }

  pattern = typeof pattern === 'undefined'
    ? this.pattern : pattern

  if (typeof pattern === 'undefined') {
    throw new TypeError('undefined pattern')
  }

  if (options.nobrace ||
    !pattern.match(/\{.*\}/)) {
    // shortcut. no need to expand.
    return [pattern]
  }

  return expand(pattern)
}
```
- example usage
```shell
...
  return
}

// step 1: figure out negation, etc.
this.parseNegate()

// step 2: expand braces
var set = this.globSet = this.braceExpand()

if (options.debug) this.debug = console.error

this.debug(this.pattern, set)

// step 3: now we have a set, so turn each one into a series of path-portion
// matching patterns.
...
```

#### <a name="apidoc.element.minimatch.Minimatch.prototype.debug"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>debug ()](#apidoc.element.minimatch.Minimatch.prototype.debug)
- description and source-code
```javascript
debug = function () {}
```
- example usage
```shell
...
this.parseNegate()

// step 2: expand braces
var set = this.globSet = this.braceExpand()

if (options.debug) this.debug = console.error

this.debug(this.pattern, set)

// step 3: now we have a set, so turn each one into a series of path-portion
// matching patterns.
// These will be regexps, except in the case of "**", which is
// set to the GLOBSTAR object for globstar behavior,
// and will not contain any / characters
set = this.globParts = set.map(function (s) {
...
```

#### <a name="apidoc.element.minimatch.Minimatch.prototype.make"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>make ()](#apidoc.element.minimatch.Minimatch.prototype.make)
- description and source-code
```javascript
function make() {
  // don't do it more than once.
  if (this._made) return

  var pattern = this.pattern
  var options = this.options

  // empty patterns and comments match nothing.
  if (!options.nocomment && pattern.charAt(0) === '#') {
    this.comment = true
    return
  }
  if (!pattern) {
    this.empty = true
    return
  }

  // step 1: figure out negation, etc.
  this.parseNegate()

  // step 2: expand braces
  var set = this.globSet = this.braceExpand()

  if (options.debug) this.debug = console.error

  this.debug(this.pattern, set)

  // step 3: now we have a set, so turn each one into a series of path-portion
  // matching patterns.
  // These will be regexps, except in the case of "**", which is
  // set to the GLOBSTAR object for globstar behavior,
  // and will not contain any / characters
  set = this.globParts = set.map(function (s) {
    return s.split(slashSplit)
  })

  this.debug(this.pattern, set)

  // glob --> regexps
  set = set.map(function (s, si, set) {
    return s.map(this.parse, this)
  }, this)

  this.debug(this.pattern, set)

  // filter out everything that didn't compile properly.
  set = set.filter(function (s) {
    return s.indexOf(false) === -1
  })

  this.debug(this.pattern, set)

  this.set = set
}
```
- example usage
```shell
...
this.pattern = pattern
this.regexp = null
this.negate = false
this.comment = false
this.empty = false

// make the set of regexps etc.
this.make()
}

Minimatch.prototype.debug = function () {}

Minimatch.prototype.make = make
function make () {
// don't do it more than once.
...
```

#### <a name="apidoc.element.minimatch.Minimatch.prototype.makeRe"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>makeRe ()](#apidoc.element.minimatch.Minimatch.prototype.makeRe)
- description and source-code
```javascript
function makeRe() {
  if (this.regexp || this.regexp === false) return this.regexp

  // at this point, this.set is a 2d array of partial
  // pattern strings, or "**".
  //
  // It's better to use .match().  This function shouldn't
  // be used, really, but it's pretty convenient sometimes,
  // when you just want to work with a regex.
  var set = this.set

  if (!set.length) {
    this.regexp = false
    return this.regexp
  }
  var options = this.options

  var twoStar = options.noglobstar ? star
    : options.dot ? twoStarDot
    : twoStarNoDot
  var flags = options.nocase ? 'i' : ''

  var re = set.map(function (pattern) {
    return pattern.map(function (p) {
      return (p === GLOBSTAR) ? twoStar
      : (typeof p === 'string') ? regExpEscape(p)
      : p._src
    }).join('\\\/')
  }).join('|')

  // must match entire pattern
  // ending in a * or ** will make it less strict.
  re = '^(?:' + re + ')$'

  // can match anything, as long as it's not this.
  if (this.negate) re = '^(?!' + re + ').*$'

  try {
    this.regexp = new RegExp(re, flags)
  } catch (ex) {
    this.regexp = false
  }
  return this.regexp
}
```
- example usage
```shell
...
files, in the style of fnmatch or glob.  If nothing is matched, and
options.nonull is set, then return a list containing the pattern itself.

'''javascript
var javascripts = minimatch.match(fileList, "*.js", {matchBase: true}))
'''

### minimatch.makeRe(pattern, options)

Make a regular expression object from the pattern.

## Options

All options are 'false' by default.
...
```

#### <a name="apidoc.element.minimatch.Minimatch.prototype.match"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>match (f, partial)](#apidoc.element.minimatch.Minimatch.prototype.match)
- description and source-code
```javascript
function match(f, partial) {
  this.debug('match', f, this.pattern)
  // short-circuit in the case of busted things.
  // comments, etc.
  if (this.comment) return false
  if (this.empty) return f === ''

  if (f === '/' && partial) return true

  var options = this.options

  // windows: need to use /, not \
  if (path.sep !== '/') {
    f = f.split(path.sep).join('/')
  }

  // treat the test path as a set of pathparts.
  f = f.split(slashSplit)
  this.debug(this.pattern, 'split', f)

  // just ONE of the pattern sets in this.set needs to match
  // in order for it to be valid.  If negating, then just one
  // match means that we have failed.
  // Either way, return on the first hit.

  var set = this.set
  this.debug(this.pattern, 'set', set)

  // Find the basename of the path by looking for the last non-empty segment
  var filename
  var i
  for (i = f.length - 1; i >= 0; i--) {
    filename = f[i]
    if (filename) break
  }

  for (i = 0; i < set.length; i++) {
    var pattern = set[i]
    var file = f
    if (options.matchBase && pattern.length === 1) {
      file = [filename]
    }
    var hit = this.matchOne(file, pattern, partial)
    if (hit) {
      if (options.flipNegate) return true
      return !this.negate
    }
  }

  // didn't get any hits.  this is success if it's a negative
  // pattern, failure otherwise.
  if (options.flipNegate) return false
  return this.negate
}
```
- example usage
```shell
...
Returns a function that tests its
supplied argument, suitable for use with 'Array.filter'.  Example:

'''javascript
var javascripts = fileList.filter(minimatch.filter("*.js", {matchBase: true}))
'''

### minimatch.match(list, pattern, options)

Match against the list of
files, in the style of fnmatch or glob.  If nothing is matched, and
options.nonull is set, then return a list containing the pattern itself.

'''javascript
var javascripts = minimatch.match(fileList, "*.js", {matchBase: true}))
...
```

#### <a name="apidoc.element.minimatch.Minimatch.prototype.matchOne"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>matchOne (file, pattern, partial)](#apidoc.element.minimatch.Minimatch.prototype.matchOne)
- description and source-code
```javascript
matchOne = function (file, pattern, partial) {
  var options = this.options

  this.debug('matchOne',
    { 'this': this, file: file, pattern: pattern })

  this.debug('matchOne', file.length, pattern.length)

  for (var fi = 0,
      pi = 0,
      fl = file.length,
      pl = pattern.length
      ; (fi < fl) && (pi < pl)
      ; fi++, pi++) {
    this.debug('matchOne loop')
    var p = pattern[pi]
    var f = file[fi]

    this.debug(pattern, p, f)

    // should be impossible.
    // some invalid regexp stuff in the set.
    if (p === false) return false

    if (p === GLOBSTAR) {
      this.debug('GLOBSTAR', [pattern, p, f])

      // "**"
      // a/**/b/**/c would match the following:
      // a/b/x/y/z/c
      // a/x/y/z/b/c
      // a/b/x/b/x/c
      // a/b/c
      // To do this, take the rest of the pattern after
      // the **, and see if it would match the file remainder.
      // If so, return success.
      // If not, the ** "swallows" a segment, and try again.
      // This is recursively awful.
      //
      // a/**/b/**/c matching a/b/x/y/z/c
      // - a matches a
      // - doublestar
      //   - matchOne(b/x/y/z/c, b/**/c)
      //     - b matches b
      //     - doublestar
      //       - matchOne(x/y/z/c, c) -> no
      //       - matchOne(y/z/c, c) -> no
      //       - matchOne(z/c, c) -> no
      //       - matchOne(c, c) yes, hit
      var fr = fi
      var pr = pi + 1
      if (pr === pl) {
        this.debug('** at the end')
        // a ** at the end will just swallow the rest.
        // We have found a match.
        // however, it will not swallow /.x, unless
        // options.dot is set.
        // . and .. are *never* matched by **, for explosively
        // exponential reasons.
        for (; fi < fl; fi++) {
          if (file[fi] === '.' || file[fi] === '..' ||
            (!options.dot && file[fi].charAt(0) === '.')) return false
        }
        return true
      }

      // ok, let's see if we can swallow whatever we can.
      while (fr < fl) {
        var swallowee = file[fr]

        this.debug('\nglobstar while', file, fr, pattern, pr, swallowee)

        // XXX remove this slice.  Just pass the start index.
        if (this.matchOne(file.slice(fr), pattern.slice(pr), partial)) {
          this.debug('globstar found match!', fr, fl, swallowee)
          // found a match.
          return true
        } else {
          // can't swallow "." or ".." ever.
          // can only swallow ".foo" when explicitly asked.
          if (swallowee === '.' || swallowee === '..' ||
            (!options.dot && swallowee.charAt(0) === '.')) {
            this.debug('dot detected!', file, fr, pattern, pr)
            break
          }

          // ** swallows a segment, and continue.
          this.debug('globstar swallow a segment, and continue')
          fr++
        }
      }

      // no match was found.
      // However, in partial mode, we can't say this is necessarily over.
      // If there's more *pattern* left, then
      if (partial) {
        // ran out of file
        this.debug('\n>>> no match, partial?', file, fr, pattern, pr)
        if (fr === fl) return true
      }
      return false
    }

    // something other than **
    // non-magic patterns just have to match exactly
    // patterns with magic have been turned into regexps.
    var hit
    if (typeof p === 'string') {
      if (options.nocase) {
        hit = f.toLowerCase() === p.toLowerCase()
      } else {
        hit = f === p
      }
      this.debug('string match', p, f, hit)
    } else {
      hit = f.match(p)
      this.debug('pattern match', p, f, hit)
    }

    if (!hit) return false
  }

  // Note: ending in / means that we'll get a final ""
  // at the end of the pattern.  This can only match a
  // corresponding "" at the end of the file.
  // If the file ends in /, then it can only match a
  // a pattern that ends in /, unless the pattern just
  // doesn't have any more for it. But, a/b/ should *not*
  // match "a/b/*", even though "" matches against the
  // [^/]*? pattern, except in partial mode, where i ...
```
- example usage
```shell
...

for (i = 0; i < set.length; i++) {
  var pattern = set[i]
  var file = f
  if (options.matchBase && pattern.length === 1) {
    file = [filename]
  }
  var hit = this.matchOne(file, pattern, partial)
  if (hit) {
    if (options.flipNegate) return true
    return !this.negate
  }
}

// didn't get any hits.  this is success if it's a negative
...
```

#### <a name="apidoc.element.minimatch.Minimatch.prototype.parse"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>parse (pattern, isSub)](#apidoc.element.minimatch.Minimatch.prototype.parse)
- description and source-code
```javascript
function parse(pattern, isSub) {
  if (pattern.length > 1024 * 64) {
    throw new TypeError('pattern is too long')
  }

  var options = this.options

  // shortcuts
  if (!options.noglobstar && pattern === '**') return GLOBSTAR
  if (pattern === '') return ''

  var re = ''
  var hasMagic = !!options.nocase
  var escaping = false
  // ? => one single character
  var patternListStack = []
  var negativeLists = []
  var stateChar
  var inClass = false
  var reClassStart = -1
  var classStart = -1
  // . and .. never match anything that doesn't start with .,
  // even when options.dot is set.
  var patternStart = pattern.charAt(0) === '.' ? '' // anything
  // not (start or / followed by . or .. followed by / or end)
  : options.dot ? '(?!(?:^|\\\/)\\.{1,2}(?:$|\\\/))'
  : '(?!\\.)'
  var self = this

  function clearStateChar () {
    if (stateChar) {
      // we had some state-tracking character
      // that wasn't consumed by this pass.
      switch (stateChar) {
        case '*':
          re += star
          hasMagic = true
        break
        case '?':
          re += qmark
          hasMagic = true
        break
        default:
          re += '\\' + stateChar
        break
      }
      self.debug('clearStateChar %j %j', stateChar, re)
      stateChar = false
    }
  }

  for (var i = 0, len = pattern.length, c
    ; (i < len) && (c = pattern.charAt(i))
    ; i++) {
    this.debug('%s\t%s %s %j', pattern, i, re, c)

    // skip over any that are escaped.
    if (escaping && reSpecials[c]) {
      re += '\\' + c
      escaping = false
      continue
    }

    switch (c) {
      case '/':
        // completely not allowed, even escaped.
        // Should already be path-split by now.
        return false

      case '\\':
        clearStateChar()
        escaping = true
      continue

      // the various stateChar values
      // for the "extglob" stuff.
      case '?':
      case '*':
      case '+':
      case '@':
      case '!':
        this.debug('%s\t%s %s %j <-- stateChar', pattern, i, re, c)

        // all of those are literals inside a class, except that
        // the glob [!a] means [^a] in regexp
        if (inClass) {
          this.debug('  in class')
          if (c === '!' && i === classStart + 1) c = '^'
          re += c
          continue
        }

        // if we already have a stateChar, then it means
        // that there was something like ** or +? in there.
        // Handle the stateChar, then proceed with this one.
        self.debug('call clearStateChar %j', stateChar)
        clearStateChar()
        stateChar = c
        // if extglob is disabled, then +(asdf|foo) isn't a thing.
        // just clear the statechar *now*, rather than even diving into
        // the patternList stuff.
        if (options.noext) clearStateChar()
      continue

      case '(':
        if (inClass) {
          re += '('
          continue
        }

        if (!stateChar) {
          re += '\\('
          continue
        }

        patternListStack.push({
          type: stateChar,
          start: i - 1,
          reStart: re.length,
          open: plTypes[stateChar].open,
          close: plTypes[stateChar].close
        })
        // negation is (?:(?!js)[^/]*)
        re += stateChar === '!' ? '(?:(?!(?:' : '(?:'
        this.debug('plType %j %j', stateChar, re)
        stateChar = false
      continue

      case ')':
        if (inClass || !patternListStack.length) {
          re += '\\)'
          continue
        }

        clearStateChar()
        hasMagic = true
        var pl = patternListStack.pop()
        // negation is (?:(?!js)[^/]*)
        // The others are (?:<pattern>)<type>
        re += pl.close
        if (pl.type === '!') {
          negativeLists.push(pl)
        }
        pl.reEnd = re.length
      continue

      case '|':
        if (inClass || !patternListStack.length || escaping) {
          re += '\\|'
          escaping = false
          continue
        }

        clearStateChar()
        re += '|'
      continue

      // these are mostly the same in regexp and ...
```
- example usage
```shell
...
  // without a try/catch and a new RegExp, but it's tricky
  // to do safely.  For now, this is safe and works.
  var cs = pattern.substring(classStart + 1, i)
  try {
    RegExp('[' + cs + ']')
  } catch (er) {
    // not a valid class!
    var sp = this.parse(cs, SUBPARSE)
    re = re.substr(0, reClassStart) + '\\[' + sp[0] + '\\]'
    hasMagic = hasMagic || sp[1]
    inClass = false
    continue
  }
}
...
```

#### <a name="apidoc.element.minimatch.Minimatch.prototype.parseNegate"></a>[function <span class="apidocSignatureSpan">minimatch.Minimatch.prototype.</span>parseNegate ()](#apidoc.element.minimatch.Minimatch.prototype.parseNegate)
- description and source-code
```javascript
function parseNegate() {
  var pattern = this.pattern
  var negate = false
  var options = this.options
  var negateOffset = 0

  if (options.nonegate) return

  for (var i = 0, l = pattern.length
    ; i < l && pattern.charAt(i) === '!'
    ; i++) {
    negate = !negate
    negateOffset++
  }

  if (negateOffset) this.pattern = pattern.substr(negateOffset)
  this.negate = negate
}
```
- example usage
```shell
...
}
if (!pattern) {
  this.empty = true
  return
}

// step 1: figure out negation, etc.
this.parseNegate()

// step 2: expand braces
var set = this.globSet = this.braceExpand()

if (options.debug) this.debug = console.error

this.debug(this.pattern, set)
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
