<template>
<div>
<div class="jumbotron jumbotron-fluid">
<div class="container-fluid">
    <h1 id="Heading" class="display-4">Twenty3 Coding Test</h1>
    <p class="lead">This data has been collected using a GET request to https://jsonplaceholder.typicode.com/users, Use the small form to call a POST request and the table to call a PUT request to replace data</p>
  </div>
</div>

<div class="container-fluid">
  <h4>Use this form to send a POST request to add a new user to the table</h4>
      <input class="user-txt" v-model="users.name" placeholder="Name"><br><br>
      <input class="user-txt" v-model="users.email" placeholder="Email"><br><br>
      <input class="user-txt" v-model="users.phone" placeholder="Phone"><br><br>
      <button class="form-btn" @click="addUser()">POST</button>
  </div>
<!-- Start of table HTML including v-for and v-bind to assign each item of data to columns -->
  <div class="container-fluid"><br>
    <h4>Use this table to send PUT requests to whatever row you wish</h4>
  <table class='table table-bordered'>
    <thead class="thead-dark">
  <tr>
    <th>ID</th>
    <th>Name</th>
    <th>Email Address</th>
    <th>Phone</th>
    <th>Confirm</th>
  </tr>
    </thead>
  <tr
    v-for="(item, index) in list"
    :key="item.id"
  >
        <td>{{item.id}}</td>
        <td><input class="user-box" v-model="list[index].name" /></td>
        <td><input class="user-box" v-model="list[index].email" /></td>
        <td><input class="user-box" v-model="list[index].phone" /></td>
        <td><button class="put-btn" @click="putUser(list[index])">PUT</button></td>
  </tr>
  </table>
  </div>
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
    //PUT Request to the API
    putUser(user) {
      axios.put('https://jsonplaceholder.typicode.com/users/${item_id}', user)
      .then(function(response)  {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      }) 
    },
  
  //POST Request to the API
 addUser() {
      axios.post('https://jsonplaceholder.typicode.com/users', { 
        name: this.users,
        email: this.email,
        phone: this.phone
      })
        .then(response => response.data)
        .catch(err => console.error("Cannot Update Properly", err))
        }
        //Request GET endpoint after POST to update table with new user data
    },

  mounted() 
  {
    //GET Request to the API
    Vue.axios.get('https://jsonplaceholder.typicode.com/users')
    .then((resp)=>{
      this.list = resp.data;
      console.warn(resp.data);
    })
  }
}

</script>

<style>
.jumbotron   {
    text-align: center;
    border-style: groove;
    border-width: 3px;
    border-color: black;
    color: white;
    font-family: Arial, Helvetica, sans-serif;
    background-color: rgba(53, 53, 93, 1);
}

.container-fluid  {
  text-align: center;
}


.h1 {
  font-family: Arial, Helvetica, sans-serif;

}

.h3 {
    font-family: Arial, Helvetica, sans-serif;
    position:relative;
    text-align: center;

}

.form-div{
  padding:10px;
  position: relative;
  left: 41%;
  right:60%;
} 

.user-txt{
  width: 300px;
  padding: 10px;
  border-style: groove;
  border-color: black;
  border-radius: 5px;
}

.user-box{
  width: 300px;
  padding: 10px;
  color: #212529;
  border-color:white;
}

.form-btn {
  width: 150px;
  position: relative;
  padding: 5px;
  border-style: groove;
  border-color: black;
  border-radius: 5px;
  margin-bottom: 10px;
}

.put-btn {
  width: 90px;
  position: static;
  padding: 5px;
}
</style>
