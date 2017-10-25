# Nuxt Auth
It is an evolution of the [@nuxtjs/auth](https://github.com/nuxt-community/auth-module) package.

## Setup
- Add `nuxt-auth` dependency using yarn or npm to your project
- Add `nuxt-auth` and `@nuxtjs/axios` to `modules` section of `nuxt.config.js`

```js
{
  modules: [
    'nuxt-auth',

     // ...Axios module should be included AFTER @nuxtjs/auth
    '@nuxtjs/axios'
 ],
 // Default Values
 auth: {
   login: {
     endpoint: 'auth/login',
     propertyName: 'token'
   },
   logout: {
     endpoint: 'auth/logout',
     method: 'GET',
     paramTokenName: '',
     appendToken: false
   },
   user: {
     endpoint: 'auth/user',
     propertyName: 'user',
     paramTokenName: '',
     appendToken: false
   },
   storageTokenName: 'nuxt-auth-token',
   tokenType: 'Bearer',
   notLoggedInRedirectTo: '/login',
   loggedInRedirectTo: '/'
 }
}
```

## Options

#### login
Set the global settings for the login action.
* **endpoint** - Set the URL of the login endpoint. It can be a relative or absolute path.
* **propertyName** - Set the name of the return object property that contains the access token.

#### logout
Sets the global settings for the logout action.
* **endpoint** - Set the URL of the logout endpoint. It can be a relative or absolute path.
* **method** - Set the request to POST or GET.
* **paramTokenName** - Set the access token query string parameter name.
* **appendToken** - Set true if you want the access token to be inserted in the URL.

#### user
Sets the global settings for the fetch action.
* **endpoint** - Set the URL of the user data endpoint. It can be a relative or absolute path.
* **propertyName** - Set the name of the return object property that contains the user data. If you want the entire object returned, set an empty string.
* **paramTokenName** - Set the access token query string parameter name.
* **appendToken** - Set true if you want the access token to be inserted in the URL.

#### storageTokenName
Set the token name in the local storage and in the cookie. 

#### tokenType
Sets the token type of the authorization header.

#### notLoggedInRedirectTo
Sets the redirect URL default of the users not logged in. This is actived when 'auth' middeware is register.

#### loggedInRedirectTo
Sets the redirect URL default of the users logged in. This is actived when 'no-auth' middeware is register.

## Example usage

```js
// ... code ...
store.dispatch('auth/login', {
  fields: {
    username: 'your_username',
    password: 'your_password'
  }
}) // run login
  
// ... code ...
store.dispatch('auth/logout') // run logout
  
// ... code ...
store.state['auth']['token'] // get access token
  
// ... code ...
store.state['auth']['user'] // get user data
  
// ... code ...
store.getters['auth/loggedIn'] // get login status (true or false)
```

## Middleware

```js
// ... in nuxt.config.js ...
router: {
  middleware: [
    'auth', // If user not logged in, redirect to '/login' or to URL defined in notLoggedInRedirectTo property
    'no-auth' // If user is already logged in, redirect to '/' or to URL defined in loggedInRedirectTo property
  ]
}
```

## License

[MIT License](./LICENSE)

Copyright (c) Nuxt Community
