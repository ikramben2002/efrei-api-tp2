Voici la version enrichie de votre README, intégrant la documentation pour la gestion des albums et des photos, tout en conservant les informations initiales sur l'API Users :

---

# API Users

## Overview
The API allows users to retrieve all of the users of the application in microservice through a REST architecture. This API will be mainly used for registered accounts.

It will also create its own users to recover data to the platform but is in no way related to the users collected via the crawling of profiles on Social Networks.

### [POST] Create User
Allows the creation of a single user.

|                            |                  |
|----------------------------|------------------|
| Requires authentication ?  | No               |
| Who can use it ?           | Owner and users  |
| Response formats           | application/json |

* HTTP request : POST → /user/create

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

* HTTP request : GET → /user/show/:id

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

# API Albums and Photos

## Objective
The goal of this exercise is to extend an existing REST API using Express.js and Mongoose. You will create models for `Album` and `Photo` and implement CRUD routes (Create, Read, Update, Delete) to manage these entities.

## Prerequisites
- An existing Express.js API setup.
- Mongoose installed and connected to a MongoDB database.
- Basic understanding of Express.js routes and Mongoose models.

## Requirements
- Node.js 16
- npm or yarn
- Git
- MongoDB (please configure `config.js` for MongoDB connection)

## Models

### Album Model
```javascript
// models/album.js
const mongoose = require('mongoose');

const albumSchema = new mongoose.Schema({
  title: { type: String, required: true },
  description: { type: String },
  photos: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Photo' }]
}, {
  collection: 'albums',
  minimize: false,
  versionKey: false
}).set('toJSON', {
  transform: (doc, ret) => {
    ret.id = ret._id;
    delete ret._id;
  }
});

module.exports = albumSchema;
```

### Photo Model
```javascript
// models/photo.js
const mongoose = require('mongoose');

const photoSchema = new mongoose.Schema({
  title: { type: String, required: true },
  url: { type: String, required: true },
  description: { type: String },
  album: { type: mongoose.Schema.Types.ObjectId, ref: 'Album', required: true }
}, {
  collection: 'photos',
  minimize: false,
  versionKey: false
}).set('toJSON', {
  transform: (doc, ret) => {
    ret.id = ret._id;
    delete ret._id;
  }
});

module.exports = photoSchema;

```

## Routes for Albums

### [GET] List All Albums
Retrieve the list of all albums.
- **HTTP Request:** GET → /albums

### [GET] Retrieve Album by ID
Retrieve a specific album by its ID.
- **HTTP Request:** GET → /albums/:id

### [POST] Create a New Album
Create a new album.
- **HTTP Request:** POST → /albums

### [PUT] Update an Existing Album
Update an album by its ID.
- **HTTP Request:** PUT → /albums/:id

### [DELETE] Delete an Album
Delete an album by its ID.
- **HTTP Request:** DELETE → /albums/:id

## Routes for Photos

### [GET] List All Photos in an Album
Retrieve all photos within a specific album.
- **HTTP Request:** GET → /albums/:albumId/photos

### [GET] Retrieve Photo by ID
Retrieve a specific photo within an album by its ID.
- **HTTP Request:** GET → /albums/:albumId/photos/:id

### [POST] Add a New Photo to an Album
Add a new photo to a specific album.
- **HTTP Request:** POST → /albums/:albumId/photos

### [PUT] Update an Existing Photo
Update a photo within a specific album by its ID.
- **HTTP Request:** PUT → /albums/:albumId/photos/:id

### [DELETE] Delete a Photo from an Album
Delete a photo from a specific album by its ID.
- **HTTP Request:** DELETE → /albums/:albumId/photos/:id

## Handling Relationships between Albums and Photos

When creating a photo, ensure it is linked to the appropriate album by updating the album's list of photos. Similarly, when deleting a photo, remove it from the album's list of photos. Utilize Mongoose's `populate` API (version 6+) to manage these relationships effectively.


## Testing Your API
Test your API using tools like Postman or cURL to ensure all routes function correctly and that relationships between albums and photos are managed properly.

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


