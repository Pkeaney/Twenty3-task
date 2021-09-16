<template>
<div>
<!--<div>
    <div
      v-for="(user, index) in users"
      :key="user.id"
      style="display: flex"
    >
      <div
        v-for="field in Object.keys(user)"
        :key="`user-field-${user.id}-${field}`"
      >
        <div v-if="field === `id`">{{ user.id }}</div>
        <input v-else v-model="users[index][field]" />
      </div>
      <button @click="update(index)">Update</button>
    </div>
  </div>-->

      <input v-model="users.name" placeholder="Name">
      <input v-model="users.email" placeholder="Email">
      <input v-model="users.phone" placeholder="Phone">

<!-- Start of table HTML including v-for and v-bind to assign each item of data to columns -->

  <table class='table table-dark table-bordered'>
  <tr>
        <td>ID</td>
        <td>Name</td>
        <td>Email Address</td>
        <td>Phone</td>
  </tr>
  <tr v-for="item in list" v-bind:key="item.id">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.email}}</td>
        <td>{{item.phone}}</td>
        <td><button>POST</button></td>
  </tr>
  </table>
  <!-- End of table -->
</div>
</template>

 <!-- Start of JS -->
<script>
//importing axios and vue axios
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

Vue.use(VueAxios,axios)

export default {
  name: "Home",
  data: () =>
   {
    return {
      users: {
        id: '',
        name: '',
        email: '', 
        phone: ''
      },
        list:'',
      }
  },
  methods:{
    
    putUser(index) {
      axios.put('https://jsonplaceholder.typicode.com/users/$user.id',this.users[index])
    },
  
 addUser() {
      axios.post('https://jsonplaceholder.typicode.com/users', {
        name: this.users.name,
        email: this.users.email,
        phone: this.users.phone
      })
        .then((response) => {
          this.isSuccess = true;
          console.log(response);
        });
 }
    },

  mounted() 
  {
    //get request to the http
    Vue.axios.get('https://jsonplaceholder.typicode.com/users')
    .then((resp)=>{
      this.list = resp.data;
      console.warn(resp.data);
    })
}

}

</script>

<style scoped>
.form {
padding: 10px;
}
</style>
