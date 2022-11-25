
---
layout: post
title: Handling Errors with Native Fetch API
readTime: 5
tags:
  - fetch
  - api
  - error-handling
---

The fetch native API is very powerful and simple to use. The downside is that it will only throw an error for network errors but not for HTTP errors such as 4xx or 5xx responses.
<!--more-->

### How `fetch()` handles error

the `fetch()` API only rejects a promise when a “network error is encountered, although this usually means permissions issues or similar.” Basically fetch() will only reject a promise if the user is offline, or some unlikely networking error occurs, such a DNS lookup failure.

### How to handle errors

The good is news is `fetch` provides a simple `ok` flag that indicates whether an HTTP response’s status code is in the successful range or not.

Our steps to handle an error could be:

1) Check response.ok
2) reject if not OK, instead of throw an error
3) Further process any error hints from server, e.g. validation issues

Example below:

```js
login() {
  const url = "https://example.com/api/users/login";
  const headers = {
    Accept: "application/json",
    "Content-Type": "application/json",
  };
  fetch(url, {
    method: "POST",
    headers,
    body: JSON.stringify({
      email: this.username,
      password: this.password,
    }),
  })
    .then((response) => {
      // 1. check response.ok
      if (response.ok) {
        return response.json();
      }
      return Promise.reject(response); // 2. reject instead of throw
    })
    .then((json) => {
      // all good, token is ready
      this.store.commit("token", json.access_token);
    })
    .catch((response) => {
      console.log(response.status, response.statusText);
      // 3. get error messages, if any
      response.json().then((json: any) => {
        console.log(json);
      })
    });
},
```


### Why do we want to use onPush?

In summary `fetch` is a simple native API for `CRUD`, and I would recommend to test it out and play around with it before going with something like `axios`.
