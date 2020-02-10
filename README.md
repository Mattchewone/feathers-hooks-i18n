# feathers-internationalisation-hook

[![Build Status](https://travis-ci.org/mattchewone/feathers-internationalisation-hook.png?branch=master)](https://travis-ci.org/mattchewone/feathers-internationalisation-hook)
[![Dependency Status](https://img.shields.io/david/mattchewone/feathers-internationalisation-hook.svg?style=flat-square)](https://david-dm.org/mattchewone/feathers-internationalisation-hook)
[![Download Status](https://img.shields.io/npm/dm/feathers-internationalisation-hook.svg?style=flat-square)](https://www.npmjs.com/package/feathers-internationalisation-hook)

> Parse internationalisation nested data for query and results

**Only tested with FeathersJS V3**

## Installation

```
npm i feathers-internationalisation-hook
```

## Complete Example

Here's an example of using the hooks

**Parsing Query**
```js
const { parseI18nQuery } = require('feathers-internationalisation-hook')

module.exports = {
  before: {
    find: [ parseI18nQuery({ fields: ['title', 'description'] }) ]
  }
}

// Query:
service.find({ query: { title: 'Post' } })
// Converts to:
params: {
  query: {
    title: {
      en: 'Post'
    }
  }
}
```

**Parsing Data**
```js
const { parseI18nData } = require('feathers-internationalisation-hook')

module.exports = {
  before: {
    find: [ parseI18nData({ fields: ['title', 'description'] }) ]
  }
}

// Create:
service.create({ title: 'Post' })
// Converts to:
params: {
  data: {
    title: {
      en: 'Post'
    }
  }
}
```

**Parsing Result**
```js
const { parseI18nQuery, parseI18nResult } = require('feathers-internationalisation-hook')

module.exports = {
  before: {
    find: [ parseI18nQuery({ fields: ['title', 'description'], language: 'fr' }) ]
  },
  after: {
    find: [ parseI18nResult({ fields: ['title', 'description'], language: 'fr' }) ]
  }
}

// Find:
service.find({ query: { title: 'Lé Post' } })
// Converts this record:
{ id: 1, title: { en: 'The Post', fr: 'Lé Post' } }
// To:
context: {
  result: {
    data: [
      { id: 1, title: 'Lé Post' }
    ]
  }
}
```

## License

Copyright (c) 2018

Licensed under the [MIT license](LICENSE).
