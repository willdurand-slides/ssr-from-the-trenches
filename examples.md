# Examples


## React

- `ReactDOMServer.renderToString()`
- That's all folks! 🤷‍♀️


## Next.js

Powerful React-based [framework](https://github.com/zeit/next.js), support
Redux.

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
<template />

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
