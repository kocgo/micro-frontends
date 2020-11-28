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

### Module Federation Plugin Setup (Container Component)
```js
/* webpack.config.js */
new ModuleFederationPlugin({
  name: 'container',
  remotes: {
    products: 'products@http://localhost:8081/remoteEntry.js'
  },
})
```

### Plugin Setup Explained  (Container Component)
```js
/* webpack.config.js */
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

### Module Federation Plugin Setup (Products Component)
```js
/* webpack.config.js */
new ModuleFederationPlugin({
  name: 'products',
  filename: 'remoteEntry.js',
  exposes: {
    /* If anyone tries to access /ProductsIndex, we give them './src/index.js' */
    "/ProductsIndex": "./src/index"
  },
})
```


### Importing Exposed Modules (Container Component)
If import statement does not match with regular modules, Webpack will look into "remotes" property in ModuleFederationPlugin configuration.
```js
/* This will go and look into "remotes" property of ModuleFederationPlugin config */
import 'products/ProductsIndex';
```

### Sharing Modules
Add "shared" property in the settings of all micro-front-ends.
```js
/* products & cart webpack.config.js */
new ModuleFederationPlugin({
  name: 'products',
  filename: 'remoteEntry.js',
  exposes: {
    /* If anyone tries to access /ProductsIndex, we give them './src/index.js' */
    "/ProductsIndex": "./src/index"
  },
  shared: ["faker"]
})
```
Once you do that, components will stop working because these shared modules will be loaded after your components.

Solution is 
- create an additional file called "bootstrap.js" and put all your code in there.
- to load your bootstrap.js asyncronously with import function.
```js
/* bootstrap.js */
import faker from 'faker';

let products = '';
```
```js
/* index.js */
import("./bootstrap");
```

