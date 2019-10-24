<template>
  <div id="app">

    <div class="parent-wrapper">
      <!-- <DropAnImage /> -->
      <DropImages />
    </div>
    
  </div>
</template>

<script>
import DropAnImage from './components/DropAnImage.vue'
import DropImages from './components/DropImages.vue'

export default {
  name: 'app',
  components: {
    DropAnImage, DropImages
  }
}
</script>


<style>
*{
  box-sizing: border-box;
}

html, body, #app{
  width:100%;
  height:100%;
  padding: 0;
  margin: 0;
  overflow: hidden;
}
body{
  background-color: #fff;
  padding:1rem;
}

.parent-wrapper{
  width:100%;
  height:300px;
}
</style>