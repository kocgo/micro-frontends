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
Examples below are based on a scenario; a "container" component calls 2 additional micro-front-ends which are called "products", "cart"

### Module Federation Plugin Setup (Webpack) (Container Component)
```js
new ModuleFederationPlugin({
  name: 'container',
  remotes: {
    products: 'products@http://localhost:8081/remoteEntry.js'
  },
})
```

### De-Composition of Plugin Setup  (Container Component)
```js
new ModuleFederationPlugin({
  name: 'container',
  remotes: {
    /* key is the renaming of the exposed module */
    products: 
       /* 'products' before '@' sign; is the name of the exposed module defined in "products" component webpack config. */
      'products@http://localhost:8081/remoteEntry.js'
  },
})
```

### Module Federation Plugin Setup (Webpack) (Products Component)
```js
new ModuleFederationPlugin({
  name: 'products',
  filename: 'remoteEntry.js'
  exposes: {
    # If anyone tries to access /ProductsIndex, we give them ;./src/index.js'
    '/ProductsIndex': './src/index'
  },
})
```


### Module Federation Plugin (How it works) (Container Component)
If any module import does not match, such as:
```js
import 'products/ProductsIndex';
```
Webpack will look into "remotes" property in ModuleFederationPlugin configuration.
