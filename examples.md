# Some examples


## React

- `ReactDOMServer.renderToString()`
- That's all folks! 🤷‍♀️


### Naive example (1/4)

```js
// server.js (express app)

app.use((req, res) => {
  const context = {};
  // 1. Create the store.
  const store = configureStore();
  // 2. Render the application using a `StaticRouter`.
  const markup = renderToString(
    <Provider store={store}>
      <StaticRouter location={req.url} context={context}>
        <App />
      </StaticRouter>
    </Provider>
  );
  // see next slide...
```
Load the application


### Naive example (2/4)

```js
  if (context.url) {
    redirect(301, context.url); // A `<Redirect>` was rendered.
  } else {
    // 3. Replace placeholders by generated state and HTML.
    const preloadedState = store.getState();
    const html = INDEX_HTML
      .replace('__SSR__', markup)
      .replace('__PRELOADED_STATE__ = {}', [
        `__PRELOADED_STATE__ =`,
        JSON.stringify(preloadedState).replace(/</g, '\\u003c'),
      ].join(' '));
    }
    res.send(html); // 4. Send the HTML to the client.
  });
});
```
Send the full HTML to the client


### Naive example (3/4)

``` diff
     <!-- index.html [...] -->

     <noscript>
       You need to enable JavaScript to run this app.
     </noscript>
-    <div id="root"></div>
+    <div id="root">__SSR__</div>
+    <script>
+      window.__PRELOADED_STATE__ = {};
+    </script>
   </body>
```
Add placeholders in the `index.html`


### Naive example (4/4)

``` diff
// src/index.js

-const store = configureStore();
+const preloadedState = window.__PRELOADED_STATE__ || {};
+// Allow the passed state to be garbage-collected
+delete window.__PRELOADED_STATE__;
+
+const store = configureStore(preloadedState);
```
Use the state generated on the server, if any


### But...

- No data fetching
- No error handling


## Next.js

Powerful React-based [framework](https://github.com/zeit/next.js), SSR-ready.

```js
class UsersList extends React.Component {

  static async getInitialProps({ store, isServer, ...props }) {
    const users = await getUsers();

    return { users };
  }

  render() {
    const { users } = this.props;
    // ...
  }
}
```


## Vue.js

- SSR is officially supported
- [ssr.vuejs.org](https://ssr.vuejs.org/en/) is pure gold

```js+vue
<!-- UsersList.vue -->
<template></template>

<script>
export default {
  asyncData ({ store }) {
    return store.dispatch('getUsers');
  }
}
</script>
```


## Nuxt.js

- Vue-based framework, inspired by Next.js
- Implement what is described in [ssr.vuejs.org](https://ssr.vuejs.org/en/)
