<template>
    <div>
        <label for="uploadmyfile">
            <p>Open the Upload dialog</p>
        </label>
        <input type="file" id="uploadmyfile" @change="requestUploadFile" />
    </div>
</template>


<script>
export default {
    methods:{
        requestUploadFile(){
            var src = this.$el.querySelector('#uploadmyfile')
            console.log(src.files)
        }
    }
}
</script>