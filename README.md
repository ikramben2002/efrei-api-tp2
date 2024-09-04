---

# API Documentation

## Overview
This API provides endpoints for managing users, albums, and photos using Express.js and Mongoose. It follows a RESTful architecture to allow CRUD (Create, Read, Update, Delete) operations on users, albums, and photos.

---

## API Users

### [POST] Create User
Allows the creation of a single user.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : POST → `/user/create`

#### Parameters :
```javascript
{
  'firstname': String, // Optional
  'lastname': String, // Optional
  'age': Number, // Optional
  'city': String // Optional
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  firstname: String,
  lastname: String,
  age: Number,
  city: String
}
```

### [GET] Show User
Show a user by ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : GET → `/user/show/:id`

#### Parameters :
```javascript
{
  id: String // Required
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  firstname: String,
  lastname: String,
  age: Number,
  city: String
}
```

---

## API Albums

### [GET] List All Albums
Retrieve the list of all albums.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : GET → `/albums`

#### Response :
```javascript
[
  {
    _id: Object_ID,
    title: String,
    description: String,
    photos: [Object_ID] // Array of photo IDs
  }
]
```

### [GET] Retrieve Album by ID
Retrieve a specific album by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : GET → `/albums/:id`

#### Parameters :
```javascript
{
  id: String // Required
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  description: String,
  photos: [Object_ID] // Array of photo IDs
}
```

### [POST] Create a New Album
Create a new album.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : POST → `/albums`

#### Parameters :
```javascript
{
  'title': String, // Required
  'description': String // Optional
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  description: String,
  photos: [] // Initially empty array
}
```

### [PUT] Update an Existing Album
Update an album by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : PUT → `/albums/:id`

#### Parameters :
```javascript
{
  'title': String, // Optional
  'description': String // Optional
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  description: String,
  photos: [Object_ID] // Updated array of photo IDs
}
```

### [DELETE] Delete an Album
Delete an album by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : DELETE → `/albums/:id`

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  description: String,
  photos: [Object_ID] // Array of photo IDs (should be empty if deleted)
}
```

---

## API Photos

### [GET] List All Photos in an Album
Retrieve all photos within a specific album.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : GET → `/albums/:albumId/photos`

#### Parameters :
```javascript
{
  albumId: String // Required
}
```

#### Response :
```javascript
[
  {
    _id: Object_ID,
    title: String,
    url: String,
    description: String,
    album: Object_ID // Album ID
  }
]
```

### [GET] Retrieve Photo by ID
Retrieve a specific photo within an album by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : GET → `/albums/:albumId/photos/:id`

#### Parameters :
```javascript
{
  albumId: String, // Required
  id: String // Required
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID // Album ID
}
```

### [POST] Add a New Photo to an Album
Add a new photo to a specific album.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : POST → `/albums/:albumId/photos`

#### Parameters :
```javascript
{
  'title': String, // Required
  'url': String, // Required
  'description': String // Optional
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID // Album ID
}
```

### [PUT] Update an Existing Photo
Update a photo within a specific album by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : PUT → `/albums/:albumId/photos/:id`

#### Parameters :
```javascript
{
  'title': String, // Optional
  'url': String, // Optional
  'description': String // Optional
}
```

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID // Album ID
}
```

### [DELETE] Delete a Photo from an Album
Delete a photo from a specific album by its ID.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : DELETE → `/albums/:albumId/photos/:id`

#### Response :
```javascript
{
  _id: Object_ID,
  title: String,
  url: String,
  description: String,
  album: Object_ID // Album ID
}
```

---

## Handling Relationships between Albums and Photos

When creating a photo, ensure it is linked to the appropriate album by updating the album's list of photos. Similarly, when deleting a photo, remove it from the album's list of photos. Utilize Mongoose's `populate` API (version 6+) to manage these relationships effectively.

### Example Using `populate`
To retrieve an album with all its photos:
```javascript
// controllers/albums.js
const AlbumModel = require('../models/album.js');

const Albums = class Albums {
  // Other methods...

  showById() {
    this.app.get('/albums/:id', async (req, res) => {
      try {
        const album = await this.AlbumModel.findById(req.params.id).populate('photos').exec();

        if (!album) {
          return res.status(404).json({ code: 404, message: 'Album not found' });
        }

        res.status(200).json(album);
      } catch (err) {
        console.error(`[ERROR] albums/showById -> ${err}`);
        res.status(400).json({ code: 400, message: 'Bad request' });
      }
    });
  }

  // Other methods...
};

module.exports = Albums;
```

## Requirements
* Node.js 16
* npm or yarn
* Git
* MongoDB (please configure `config.js` for MongoDB connection)

## Install
```bash
yarn install
```

## Production Mode
```bash
yarn prod
```

## Development Mode
```bash
yarn dev
```

---
