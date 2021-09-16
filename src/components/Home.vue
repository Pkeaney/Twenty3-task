<template>
<div>
</div>
</template>

<script>
//importing axios and vue axios
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

Vue.use(VueAxios,axios)

export default {
  name: "Home",
  data()  {
    return {list:undefined}
  },
  mounted() 
  {
    //get request to the http
    Vue.axios.get('https://jsonplaceholder.typicode.com/users')
    .then((resp)=>{
      this.list = resp
      console.warn(resp)
    })
}
}
</script>

<style scoped></style>
