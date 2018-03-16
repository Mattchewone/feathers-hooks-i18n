# feathers-i18n-hook

[![Build Status](https://travis-ci.org/mattchewone/feathers-i18n-hook.png?branch=master)](https://travis-ci.org/mattchewone/feathers-i18n-hook)
[![Code Climate](https://codeclimate.com/github/mattchewone/feathers-i18n-hook/badges/gpa.svg)](https://codeclimate.com/github/mattchewone/feathers-i18n-hook)
[![Test Coverage](https://codeclimate.com/github/mattchewone/feathers-i18n-hook/badges/coverage.svg)](https://codeclimate.com/github/mattchewone/feathers-i18n-hook/coverage)
[![Dependency Status](https://img.shields.io/david/mattchewone/feathers-i18n-hook.svg?style=flat-square)](https://david-dm.org/mattchewone/feathers-i18n-hook)
[![Download Status](https://img.shields.io/npm/dm/feathers-i18n-hook.svg?style=flat-square)](https://www.npmjs.com/package/feathers-i18n-hook)

> Parse i18n nested data for query and results

## Installation

```
npm i feathers-i18n-hook
```

## Documentation

TBD

## Complete Example

Here's an example of using the hooks

Parsing Query
```js
const { parseI18nQuery } = require('feathers-i18n-hook')

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

Parsing Data
```js
const { parseI18nData } = require('feathers-i18n-hook')

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

Parsing Result
```js
const { parseI18nQuery, parseI18nResult } = require('feathers-i18n-hook')

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
