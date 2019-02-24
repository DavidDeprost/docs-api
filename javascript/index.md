---
title: "Javascript Client Libraries"
date: "2019-01-09"
meta_title: "Javascript Content API Client Libarary – Ghost"
meta_description: "Ghost provides a flexible promise-based JavaScript library for accessing the Content API which can be used in any JavaScript project. Read more on Ghost Docs 👉"
keywords:
    - "headless cms"
    - "javascript"
    - "ghost api"
sidebar: "javascript"
---

This is a blurb introduction thing.


And then a bit more info.

## Content API

Ghost provides a flexible promise-based JavaScript library for accessing the Content API. The library can be used in any JavaScript project, client or server side and abstracts away all the pain points of working with API data.

## Working Example

```javascript
const api = new GhostContentAPI({
  host: 'https://demo.ghost.io',
  key: '22444f78447824223cefc48062',
  version: 'v2'
});

// fetch 5 posts, including related tags and authors
api.posts
    .browse({limit: 5, include: 'tags,authors'})
    .then((posts) => {
        posts.forEach((post) => {
            console.log(post.title);
        });
    })
    .catch((err) => {
        console.error(err);
    });
```

## Authentication

The client requires the host address of your Ghost API, a Content API key, and a version string in order to authenticate.

- `host` - API domain, must not end in a trailing slash.
- `key` - hex string copied from the "Integrations" screen in Ghost Admin
- `version` - should be set to 'v2'

See the documentation on [Content API authentication](/api/content/#authentication) for more explanation.

## Endpoints

All endpoints & parameters provided by the [Content API](/api/content/) are supported.

```javascript
// Browsing posts returns Promise([Post...]);
// The resolved array will have a meta property
api.posts.browse({limit: 2, include: 'tags,authors'});
api.posts.browse();

// Reading posts returns Promise(Post);
api.posts.read({id: 'abcd1234'});
api.posts.read({slug: 'something'}, {formats: ['html', 'plaintext']});

// Browsing authors returns Promise([Author...])
// The resolved array will have a meta property
api.authors.browse({page: 2});
api.authors.browse();

// Reading authors returns Promise(Author);
api.authors.read({id: 'abcd1234'});
api.authors.read({slug: 'something'}, {include: 'count.posts'}); // include can be array for any of these

// Browsing tags returns Promise([Tag...])
// The resolved array will have a meta property
api.tags.browse({order: 'slug ASC'});
api.tags.browse();

// Reading tags returns Promise(Tag);
api.tags.read({id: 'abcd1234'});
api.tags.read({slug: 'something'}, {include: 'count.posts'});

// Browsing pages returns Promise([Page...])
// The resolved array will have a meta property
api.pages.browse({limit: 2});
api.pages.browse();

// Reading pages returns Promise(Page);
api.pages.read({id: 'abcd1234'});
api.pages.read({slug: 'something'}, {fields: ['title']});

// Browsing settings returns Promise(Settings...)
// The resolved object has each setting as a key value pair
api.settings.browse();
```

For all resources except settings, the `browse()` method will return an array of objects, and the `read()` method will return a single object. The `settings.browse()` endpoint always returns a single object with all the available key-value pairs.

See the documentation on [Content API resources](/api/content/#resources) for a full description of the response for each resource.

## Installation

`yarn add @tryghost/content-api`

`npm install @tryghost/content-api`

You can also use the standalone UMD build:

`https://unpkg.com/@tryghost/content-api@{version}/umd/content-api.min.js`

### Usage

ES modules:

```javascript
import GhostContentAPI from '@tryghost/content-api'
```

Node.js:

```javascript
const GhostContentAPI = require('@tryghost/content-api');
```

In the browser:

```html
<script src="https://unpkg.com/@tryghost/content-api@{version}/umd/content-api.min.js"></script>
<script>
    const api = new GhostContentAPI({
        // authenticate here
    });
</script>
```

Get the [latest version](https://unpkg.com/@tryghost/content-api) from [unpkg.com](https://unpkg.com).

----

# Admin API

Admin API keys should remain secret, and therefore this promise-based JavaScript library is designed for server-side usage only. This library handles all the details of generating correctly formed urls and tokens, authenticating and making requests.

## Working Example

```javascript
const api = new GhostAdminPI({
  host: 'https://demo.ghost.io',
  key: 'secret_id:with_secret_key',
  version: 'v2'
});

...
```

## Authentication

The client requires the host address of your Ghost API, an Admin API key, and a version string in order to authenticate.

- `host` - API domain, must not end in a trailing slash.
- `key` - string copied from the "Integrations" screen in Ghost Admin
- `version` - should be set to 'v2'

See the documentation on [Admin API authentication](/api/admin/#authentication) for more explanation.

## Endpoints

All endpoints & parameters provided by the [Admin API](/api/admin/) are supported.

```javascript

// [Stability: stable]

// Browsing posts returns Promise([Post...]);
// The resolved array will have a meta property
api.posts.browse();
api.posts.read({id: 'abcd1234'});
api.posts.add...
api.posts.edit...
api.posts.delete...

// Browsing pages returns Promise([Page...])
// The resolved array will have a meta property
api.pages.browse({limit: 2});
api.pages.read({id: 'abcd1234'});
api.pages.add...
api.pages.edit...
api.pages.delete...

api.images...

// [Stability: experimental]

api.users...
api.subscribers...
api.themes...
api.configuration...
api.webhooks...
...

```


## Installation

`yarn add @tryghost/admin-api`

`npm install @tryghost/admin-api`


### Usage

ES modules:

```javascript
import GhostAdminAPI from '@tryghost/admin-api'
```

Node.js:

```javascript
const GhostAdminAPI = require('@tryghost/admin-api');
```
