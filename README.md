<img src="http://rawgit.com/caiogondim/webpack-conditional-loader/master/logo/banner.svg" width="100%" />

# webpack-conditional-loader-ng

<div>
  <a href="https://www.npmjs.com/package/webpack-conditional-loader-ng"><img src="https://img.shields.io/npm/v/webpack-conditional-loader.svg" /></a>
</div>

<br>

Forked from webpack-conditional-loader and made some improvements.

Inspired by [C conditionals directive](https://gcc.gnu.org/onlinedocs/gcc-3.0.2/cpp_4.html),
conditional loader decides if a given block should be included in the final bundle.

Useful for removing instrumentation code and making your final production bundle smaller (therefore
faster).

## Installation

```bash
npm install --save-dev webpack-conditional-loader-ng
```

## Usage

### In your `webpack.config.js`

Put `webpack-conditional-loader-ng` as the last loader in the array, so it will process the code before
all others.

```js
module: {
  rules: [{
    test: /\.js$/,
    use: ['babel-loader', 'webpack-conditional-loader-ng']
  }]
}
```

Get an example config file [here](https://github.com/mikewootc/webpack-conditional-loader-ng/blob/master/webpack.js)

### On your code

Use `// #if expression` and `// #endif` to wrap blocks of code you want to be removed if a given
predicate is false.

```js
// #if process.env.NODE_ENV === 'DEVELOPMENT'
console.log('lorem')
console.log('ipsum')
// #endif
```

In the example above, the code will be removed if the enviroment variable `NODE_ENV` is not
`DEVELOPMENT`, removing unnecessary code from your production bundle.

The same technique can be used to prevent loading packages in the production bundle.

```js
// #if process.env.NODE_ENV !== 'BUILD'
import reduxLogger from 'redux-logger'
// #endif
```

## Credits
- [GCC C conditional documentation](https://gcc.gnu.org/onlinedocs/gcc-3.0.2/cpp_4.html)

---

[caiogondim.com](https://caiogondim.com) &nbsp;&middot;&nbsp;
GitHub [@caiogondim](https://github.com/caiogondim) &nbsp;&middot;&nbsp;
Twitter [@caio_gondim](https://twitter.com/caio_gondim)
