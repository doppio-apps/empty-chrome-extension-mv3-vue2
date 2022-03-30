# ☕ Doppio Labs - Empty Chrome Extension

See [Visit ☕ Doppio Labs! ☕ ](https://doppio.app).

## Fully working with Manifest v3

### Ingredients

- Vue v2
- Vuex
- Vue-cli-plugin-browser-extension

## Project setup

```
yarn install
```

After `yarn install` move 3x files from `config_files` folder:

1. `index.js` to `node_modules`->`vue-cli-plugin-browser-extension`
2. `manifest.js` to `node_modules`->`vue-cli-plugin-browser-extension`->`lib`
3. `webpack-extension-reloader.js` to `node_modules`->`vue-cli-plugin-browser-extension`->`lib`

### Compiles and hot-reloads for development

```
yarn serve
```

### Compiles and minifies for production

```
yarn build
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
