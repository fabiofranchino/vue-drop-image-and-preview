# Vue.js component to drag&drop images with preview

This is not a complete component but rather a starting point to customize something more complex.
They are examples about how to allow users drop images in the browser in a Vue app.
There are two flavuors:
- `DropAnImage` to allow one image
- `DropImages` allows many images to be dropped

## Usage

```html
<template>
  <div id="app">
      <DropAnImage />
  </div>
</template>

<script>
import DropAnImage from './components/DropAnImage.vue'

export default {
  components: {
    DropAnImage
  }
}
</script>
```



# Development

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
