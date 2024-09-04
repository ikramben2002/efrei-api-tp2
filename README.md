# API Documentation

## Overview

This API provides endpoints for managing users, albums, and photos using Express.js and Mongoose. It follows a RESTful architecture to allow CRUD (Create, Read, Update, Delete) operations on users, albums, and photos.

## API Users

### [POST] Create user

Allows the creation of a single user.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `POST /user/create`

#### Parameters:
```javascript
{
  'firstname': String, // Optional
  'lastname': String, // Optional
  'age': Number, // Optional
  'city': String // Optional
}
```

#### Response:
```javascript
{
  _id: Object_ID,
  firstname: String,
  lastname: String,
  age: Number,
  city: String
}
```

### [GET] Show user

Shows a user by ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `GET /user/show/:id`

#### Parameters:
```javascript
{
  id: String // Required
}
```

#### Response:
```javascript
{
  _id: Object_ID,
  firstname: String,
  lastname: String,
  age: Number,
  city: String
}
```

## API Albums

### [POST] Create album

Allows the creation of a single album.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `POST /album`

#### Parameters:
```javascript
{
  'title': String, // Required
  'description': String, // Optional
  'photos': [Object_ID] // Optional, Array of Photo IDs
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  description: String,
  photos: [Object_ID]
}
```

### [GET] Show album by ID

Retrieve an album by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `GET /album/:id`

#### Parameters:
```javascript
{
  id: String // Required
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  description: String,
  photos: [Object_ID]
}
```

### [GET] List all albums

Retrieve a list of all albums.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `GET /albums`

#### Response:
```javascript
[
  {
    id: Object_ID,
    title: String,
    description: String,
    photos: [Object_ID]
  },
  // More albums...
]
```

### [PUT] Update album

Update an existing album by ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `PUT /album/:id`

#### Parameters:
```javascript
{
  'title': String, // Optional
  'description': String, // Optional
  'photos': [Object_ID] // Optional, Array of Photo IDs
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  description: String,
  photos: [Object_ID]
}
```

### [DELETE] Delete album

Delete an album by ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `DELETE /album/:id`

#### Parameters:
```javascript
{
  id: String // Required
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  description: String,
  photos: [Object_ID]
}
```

## API Photos

### [POST] Create photo

Allows the creation of a single photo within an album.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `POST /album/:albumId/photo`

#### Parameters:
```javascript
{
  'title': String, // Required
  'url': String, // Required
  'description': String, // Optional
  'album': Object_ID // Required, Album ID
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID
}
```

### [GET] Show photo by ID

Retrieve a photo by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `GET /photo/:id`

#### Parameters:
```javascript
{
  id: String // Required
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID
}
```

### [GET] List all photos in an album

Retrieve a list of all photos within a specific album.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `GET /album/:albumId/photos`

#### Response:
```javascript
[
  {
    id: Object_ID,
    title: String,
    url: String,
    description: String,
    album: Object_ID
  },
  // More photos...
]
```

### [PUT] Update photo

Update an existing photo by ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `PUT /photo/:id`

#### Parameters:
```javascript
{
  'title': String, // Optional
  'url': String, // Optional
  'description': String, // Optional
  'album': Object_ID // Optional, Album ID
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID
}
```

### [DELETE] Delete photo

Delete a photo by ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request: `DELETE /photo/:id`

#### Parameters:
```javascript
{
  id: String // Required
}
```

#### Response:
```javascript
{
  id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID
}
```

## Requirements

* Node.js 16+
* npm or yarn
* Git
* MongoDB (please configure `config.js` to link MongoDB)

## Install

```bash
yarn install
```

## Production mode

```bash
yarn prod
```

## Dev mode

```bash
yarn dev
```

---
