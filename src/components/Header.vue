<template>
<ul>
  <li><router-link class="active" to="/">Home</router-link></li>
  <li><router-link to="/add">Add Restaurant</router-link></li>
  <li><router-link to="/logout" v-on:click="logout">Logout</router-link></li>
</ul>
</template>

<script>
// import router from '@/routes';
// import { RouterLink } from 'vue-router';
export default {
    name:'Header',
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>

<style>
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
}

li {
  float: left;
}

li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

li a:hover:not(.active) {
  background-color: #111;
}

.active {
  background-color: #04AA6D;
}

</style>