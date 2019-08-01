# front-matter
[![build][build-img]][build-url]
[![coverage][coverage-img]][coverage-url]
[![npm][npm-img]][npm-url]
[![github][github-img]][github-url]

[![Sauce Test Status](https://saucelabs.com/browser-matrix/front-matter.svg)](https://saucelabs.com/u/front-matter)

> Extract meta data (front-matter) from documents.

This modules does not do any IO (file loading or reading), only extracting and
parsing front matter from strings.

This concept that was originally introduced to me through the [jekyll][jekyll] blogging system and is pretty useful where you want to be able to easily add meta-data to content without the need for a database. YAML is extracted from the the top of a file between matching separators of "---" or "= yaml =". It will also extract YAML between a separator and "...".

<!-- This is part of a long running project I have been working on where I am splitting out internals of [haiku][haiku] into to separate, more useful and shareable modules. If your in need of a static site generator [check it out][haiku]. -->

# Install

With [npm][npm] do:

    npm install front-matter

# Example

So you have a file `example.md`:

```yaml
---
title: Just hack'n
description: Nothing to see here
---

This is some text about some stuff that happened sometime ago
```

**NOTE:** As of `front-matter@2.0.0` valid front matter is considered to have
the starting separator on the first line.

Then you can do this:

```javascript
var fs = require('fs')
  , fm = require('front-matter')

fs.readFile('./example.md', 'utf8', function(err, data){
  if (err) throw err

  var content = fm(data)

  console.log(content)
})
```

And end up with an object like this:

```javascript
{
    attributes: {
        title: 'Just hack\'n',
        description: 'Nothing to see here'
    },
    body: '\nThis is some text about some stuff that happened sometime ago',
    frontmatter: 'title: Just hack\'n\ndescription: Nothing to see here'
}
```

# Methods

```javascript
var fm = require('front-matter')
```

## fm(string)

Return a `content` object with two properties:

* `content.attributes` contains the extracted yaml attributes in json form
* `content.body` contains the string contents below the yaml separators
* `content.frontmatter` contains the original yaml string contents

# fm.test(string)

Check if a string contains a front matter header of "---" or "= yaml =". Primarily used internally but is useful outside of the module.

Returns `true` or `false`

