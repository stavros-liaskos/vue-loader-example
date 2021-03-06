# vue-loader example

> Example using [vue-loader](https://github.com/vuejs/vue-loader) with [Webpack](http://webpack.github.io).

## Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# run unit tests
npm test
```


### sass/scss&postcss
```
vue: {
  loaders: {
    js: 'babel!eslint',
    scss: 'style!css!sass!postcss'
  },
  postcss: [require('cssnext')(),require('postcss-nested')(),require('postcss-mixins')()]
}

<style scoped lang="scss">
.red{
  .test{
    color:blue !important;
    transform:rotateX(30deg) rotateY(30deg) translateY(50px);
  }
}
</style>

<!-- retult: -->
<style>
.red .test[_v-3def8906]{
    color: blue !important;
    -webkit-transform: rotateX(30deg) rotateY(30deg) translateY(50px);
    transform: rotateX(30deg) rotateY(30deg) translateY(50px);
}
</style>
```

#### ES2015 by Default

`vue-loader` automatically applies Babel transforms to the JavaScript inside `*.vue` components. Write ES2015 today!

The default Babel options used for Vue.js components are:

``` js
{
  presets: ['es2015'],
  plugins: ['transform-runtime']
}
```

If you wish to mofidy this, you can add a `babel` field in your webpack config, which will be merged with the default options. For example:

``` js
// webpack.config.js
module.exports = {
  // other configs...
  babel: {
    // enable stage-0 features, make sure to install
    // babel-preset-stage-0
    presets: ['es2015', 'stage-0'],
    plugins: ['transform-runtime']
  }
}
```

#### Using Per-file Pre-processors

If you only want to use pre-processors in a specific file, you can add an inline `lang` attribute to a language block:

``` html
<style lang="stylus">
  /* use stylus here */
</style>
```

Note you will have to install `stylus-loader` so that Webpack can handle the compilation. The `lang` attribute will be used to automatically locate the loader to use, and you can pass Webpack loader queries in it as well:

``` html
<style lang="sass?outputStyle=expanded">
  /* use sass here with expanded output */
</style>
```

#### Scoped CSS

> Experimental. Requires `vue-loader` ^4.0.0

You can add the `scoped` attribute to a `<style>` block to make it scoped to the current component. A few things to take note:

1. You can include both scoped and non-scoped styles in the same component.

2. A child component's root node will be affected by both the parent's scoped CSS and the child's scoped CSS.

3. Partials are not affected by scoped styles.
