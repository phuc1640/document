# Implementation
## Backend
### Need 3 apis
* Login
* Refresh access token
* Logut

#### Login
* Return access token in response body
* Return refresh token in response header cookie(**HttpOnly**)

#### Refresh access token
* Read and verify the token in the request cookies
* Send a new access token in response body
* Send a new refresh token in response header cookie(**HttpOnly**)

#### Logut
* Delete refresh access token in the cookie

## Frontend
### When login
* Save the Access token in a variable

### When making a request
1. Check to see if the Access token is existed or expired
   * If it is, call the Refresh access token api(**with cookie attached**)
     * Save the new Access token
2. Make the request

### When logut
1. Call the logout api
2. Delete the Access token
3. Use the browser [storage event](https://javascript.info/localstorage#storage-event) to logout for multiple tabs

**Example**
```
window.addEventListener('storage', this.syncLogout)

// ......

syncLogout (event) {
  if (event.key === 'logout') {
    console.log('logged out from storage!')
    Router.push('/login')
  }
}

// ......

async function logout () {
  inMemoryToken = null;
  const url = 'http://localhost:3010/auth/logout'
  const response = await fetch(url, {
    method: 'POST',
    credentials: 'include',
  })
  // to support logging out from all windows
  window.localStorage.setItem('logout', Date.now())
}
```

## Bonus

### To force logut for a specific user
**Set a version control for the token**
