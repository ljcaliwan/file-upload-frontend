<template>
  <div class="app">
    <form ref="upload" @submit.prevent="submit">
      <input
        type="file"
        ref="uploadFile"
        @change="onFileUpload()"
        class="form-control"
        required
      />
      <input type="button" @click="startUpload" name="Upload" value="Upload" />
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    data: () => ({
        formData: null
    }),
    methods: {
        onFileUpload(){
            let file = this.$refs.uploadFile.files[0]
            this.formData = new FormData()
            this.formData.append("file", file)
        },
        startUpload(){
            axios({
                url: 'http://localhost:8080/upload',
                method: 'POST',
                data: this.formData,
                headers: {
                    Accept: 'application/json',
                    'Content-Type': 'multipart/form-data'
                },
            }).then(response => {
                console.log(JSON.stringify(response.data))
            });
        }

    }
};

</script>

<style scoped>
</style>