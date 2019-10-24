<template>
  <div class="drop" 
    :class="getClasses" 
    @dragover.prevent="dragOver" 
    @dragleave.prevent="dragLeave"
    @drop.prevent="drop($event)">

      <img :src="imageSource" v-if="imageSource" />
      <h1 v-if="wrongFile">Wrong file type</h1>
      <h1 v-if="!imageSource && !isDragging && !wrongFile">Drop an image</h1>

  </div>
</template>



<script>
export default {
  name: 'DropAnImage',
  data(){
    return{
      isDragging:false,
      wrongFile:false,
      imageSource:null
    }
  },
  computed:{
    getClasses(){
      return {isDragging: this.isDragging}
    }
  },
  methods:{
    dragOver(){
      this.isDragging = true
    },
    dragLeave(){
      this.isDragging = false
    },
    drop(e){
      let files = e.dataTransfer.files

      this.wrongFile = false

      // allows only 1 file
      if (files.length === 1) {

        let file = files[0]

        // allows image only
        if (file.type.indexOf('image/') >= 0) {

          var reader = new FileReader()
          reader.onload = f => {
            this.imageSource = f.target.result
            this.isDragging = false
          }
          reader.readAsDataURL(file)
        }else{
          this.wrongFile = true
          this.imageSource = null
          this.isDragging = false
        }
      }
    }
  }
}
</script>



<style scoped>
.drop{
  width: 100%;
  height: 100%;
  background-color: #eee;
  border:10px solid #eee;

  display: flex;
  align-items: center;
  justify-content: center;

  padding: 1rem;
  transition: background-color .2s ease-in-out;

  font-family: sans-serif;
}

.isDragging{
  background-color: #999;
  border-color: #fff;
}

img{
  width: 100%;
  height: 100%;
  object-fit: contain;
}
</style>
