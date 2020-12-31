# XpresserJs Frontend Helpers

Create a javascript file of all **named routes** that can be imported and bundled by webpack.

## Problem

When working with lots of routes, Sometimes you find it difficult to remember the url of your routes And the glorious
xpresser `$.helpers.route()` helper function that converts names to urls can't be accessed in Frontend.

For Example, we have a route like this
Backend
```javascript
$.router.get('/user/:userId/uploads/:fileId/') // /user/164/song/733
```

In our Frontend

```javascript
axios.get(`/user/${userId}/uploads/${fileId}`)
```

Remembering **urls, required/un-required route named parameters** when you have over **500 routes** will be difficult.

## Solution

AUTOGENERATED routes file that can be imported into your Frontend. This plugin reads your routes then generates a file
that can be configured to use any `Http Library` you are using. This file includes all your routes as a Library.

For example using the same example above, But we have to add a name to identify the route.

```javascript
Backend
router.get('/user/:userId/uploads/:fileId/', http => {
  return {file: 'image.png'}
}).name('uploaded_file') // /user/164/song/733

// Simple Routes

```

In your frontend

```javascript
import ServerRequests from "./auto-generated-file";

await ServerRequests.get.uploaded_file([userId, songId]); // returns {"file": "image.png"}
```

### More Examples
Backend
```javascript
router.get('/users', 'UserController@users').name('users');
router.post('/users', 'UserController@create').name('user.create');

router.get('/user/:userId', 'UserController@user').name('user');
router.patch('/user/:userId', 'UserController@update').name('user.update');
router.delete('/user/:userId', 'UserController@delete').name('user.delete');

router.get('/songs/:genre/:year?/:month?/:day?').name('songs');
```

Frontend.

```javascript
import ServerRequests from "./auto-generated-file";

await ServerRequests.get.users({page: 2}) // GET: /user?page=2
await ServerRequests.post.users({
  id: 35, name: "John Doe", email: "newuser@app.me", password: "password"
}) // POST: /users with body

await ServerRequests.get.user(35) // GET: /user/35
await ServerRequests.patch.user(35, {
  password: "newPassword"
}) // PATCH: /user/35
await ServerRequests.delete.user(35) // DELETE: /user/35

await ServerRequests.get.songs(["hip-hop", 2020, 4, 15]) // GET: /songs/hip-hop/2020/4/15
```

## What you get.

- Autocomplete for faster development.
- It will never make a `Http Verb` mistake like send `get` instead of `post`.
- Easily supports any http library.

This came like an idea to me, so I decided to bring it to life.
Note: this is still experimental. I have lots of work on my table so i won't be paying attention to it for now...
I will be updating my local version during my day-to-day use then someday i will update this.

For now, it only generates the file. you have to configure it to work like the Examples above. 🤦‍♂️