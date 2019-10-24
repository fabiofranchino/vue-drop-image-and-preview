<template>
  <div class="drop" 
    :class="getClasses" 
    @dragover.prevent="dragOver" 
    @dragleave.prevent="dragLeave"
    @drop.prevent="drop($event)">

        <div class="img" v-for="img in imageSources">
            <img :src="img" />
        </div>
        

      <h1 v-if="imageSources.length == 0 && !isDragging">Drop some images</h1>

  </div>
</template>



<script>
export default {
  name: 'DropImages',
  data(){
    return{
        isDragging:false,
        imageSources:[]
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
    async drop(e){
        let files = [...e.dataTransfer.files]
        let images = files.filter(file => file.type.indexOf('image/') >= 0)
        let promises = []
        images.forEach(file => {
            promises.push(this.getBase64(file))
        })

        let sources = await Promise.all(promises)
        this.imageSources = this.imageSources.concat(sources)
        this.isDragging = false
    },

    getBase64(file) {
        const reader = new FileReader()
        return new Promise(resolve => {
            reader.onload = ev => {
                resolve(ev.target.result)
            }
            reader.readAsDataURL(file)
        })
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

  overflow: hidden;
}

.isDragging{
  background-color: #999;
  border-color: #fff;
}

.img{
    padding:1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
}

img{
  width: 100%;
  height: 100%;
  object-fit: contain;
}
</style>
