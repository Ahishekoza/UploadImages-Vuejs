<template>
  <div class="m-2 h5">
    <form @submit.prevent="handleSubmit" enctype="multipart/form-data">
      <div class="d-flex flex-column gap-2">
        <label for="file" >Upload Files</label>
        <input type="file" ref="file" @change="handleChange" />
      </div>
      <div v-if="file" class="my-2">{{ this.file.name }}</div>
      <div :class="[file ? '' : 'mt-2']">
        <button class="btn btn-primary">Submit</button>
      </div>
    </form>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  name: "SimpleUpload",
  data(){
    return{
        file:""
    }
  },
  methods:{
    handleChange(){
        this.file=this.$refs.file.files[0]
        console.log(this.file.name)
    },
    async handleSubmit(){
        
        const formData =  new FormData()
        formData.append('file',this.file)

        await axios.post('/api',formData,{
            headers:{"Content-Type":"multipart/form-data"}
        }).then((response)=>{
            console.log(response)
        }).catch((error)=>{
            console.log(error)
        })

        
    }
  }
};
</script>
