<template>
<Header />    
<h1>Home Page</h1>
<h3>Hello {{ name }}, Welcome to Add Restaurant Page</h3>

<table id="customers">
  <tr>
    <th>ID</th>
    <th>NAME</th>
    <th>ADDRESS</th>
    <th>CONTACT</th>
    <th>UPDATE</th>
    <th>DELETE</th>
  </tr>
  <tr v-for="item in restaurants" :key="item.id">
    <td>{{ item.id }}</td>
    <td>{{ item.name }}</td>
    <td>{{ item.address }}</td>
    <td>{{ item.contact }}</td>
    <td><router-link :to="'/update/' + item.id">Update</router-link></td>
    <td><button v-on:click="deleteRestaurant(item.id)">DELETE</button></td>
  </tr>
</table>

</template>

<script>
import axios from 'axios';
import Header from '../components/Header.vue';

export default{
    name:"Home",
    components:{
        Header,
    },

    data()  // This is use to show user's name on beside welcome text
    {
    return{
        name:'',          // Used to show the user's name on home page
        restaurants:[],   // Used to store the restaurants data
    }
    },

    methods:{
      async deleteRestaurant(id)
      {
        let result = await axios.delete ("http://localhost:3000/restaurants/"+id); 
        if(result.status==200)
        {
          this.loadData()
        }
      },

      async loadData()
      {
        let user = localStorage.getItem('user-info');       
        this.name= JSON.parse(user).name  // This is use to show user's name on beside welcome test
        if(!user)                                          // if user not present in local storage then redirect it to the SignUp page     
        {
            this.$router.push({name:'SignUp'})
        }

        let result = await axios.get ("http://localhost:3000/restaurants")
        console.log(result)
        this.restaurants= result.data
      }
    },

    mounted()  // In mount page will load First
    {                                                                              
      this.loadData()
    }    
}
</script>

<style>

#customers {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

#customers td, #customers th {
  border: 1px solid #ddd;
  padding: 8px;
}

#customers tr:nth-child(even){background-color: #f2f2f2;}

#customers tr:hover {background-color: #ddd;}

#customers th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #04AA6D;
  color: white;
}

</style>