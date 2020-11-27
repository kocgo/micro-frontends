# Micro Frontends with React

### Resources
```
https://www.udemy.com/course/microfrontend-course/
https://martinfowler.com/articles/micro-frontends.html
```

### Types of integration
1) Built-time Integration
2) Run-Time Integration (via Iframe, Web Components, JavaScript)
3) Server-side template composition

### Examples
Examples below are based on a scenario; a container component calls 2 additional micro-front-ends which are called "products", "cart"

### Module Federation Plugin (Webpack)
```js
new ModuleFederationPlugin({
  name: 'container',
  remotes: {
    products: 'products@http://localhost:8081/remoteEntry.js'
  },
})
```
