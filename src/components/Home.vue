<template>
<div><br>
<h4>Enter data to fields to create or update data:</h4>
  <div class="form-group">
  <form>
      <input v-model="users.name" placeholder="Name">
      <input v-model="users.email" placeholder="Email">
      <input v-model="users.phone" placeholder="Phone">
      <button @click="addUser()">POST</button>
  </form>
  </div>
<!-- Start of table HTML including v-for and v-bind to assign each item of data to columns -->

  <table class='table table-dark table-bordered'>
  <tr>
    <th>ID</th>
    <th>Name</th>
    <th>Email Address</th>
    <th>Phone</th>
  </tr>
  <tr
    v-for="(item, index) in list"
    :key="item.id"
  >
        <td>{{item.id}}</td>
        <td><input v-model="list[index].name" /></td>
        <td><input v-model="list[index].email" /></td>
        <td><input v-model="list[index].phone" /></td>
        <td><button @click="putUser(list[index])">PUT</button></td>
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
        name: '',
        email: '', 
        phone: ''
      },
      list:[],
      }
  },
  methods:{
    
    putUser(user) {
      axios.put('https://jsonplaceholder.typicode.com/users', user)
      .then(function(response)  {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      }) 
    },
  
 addUser() {
      axios.post('https://jsonplaceholder.typicode.com/users', { 
        name: this.users,
        email: this.email,
        phone: this.phone
      })
        .then((response) => {
          console.log(response);
        })
        .catch(e => {
          this.errors.push(e)
        })
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
