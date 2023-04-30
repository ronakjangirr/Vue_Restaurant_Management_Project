<template>
    <img class="logo" src="../assets/resto-logo.png"/>
<h3>Login Page</h3>
<div class="login">
    <input type="text" v-model="email" placeholder="Enter Email"/>
    <input type="password" v-model="password" placeholder="Enter Password"/>
    <button v-on:click="login">Login</button>
    <p><router-link to="/sign-up">Sign up</router-link></p>
</div>
</template>

<script>
import axios from 'axios';
export default {
    name: "SignUp",
    data()
    {

    return{
        email:'',
        password:''
    }
    },
    
    methods:{
        async login()
        {
            let result= await axios.get(
                `http://localhost:3000/users?email=${this.email}&password=${this.password}`
                );
        if(result.status==200 && result.data.length > 0)
            {
            localStorage.setItem("user-info", JSON.stringify(result.data[0]));
            this.$router.push({name:"Home"})
            }    
    },

    mounted()
    {
        let user = localStorage.getItem('user-info');
        if(user)
        {
            this.$router.push({name:'Home'})
        }
    }
    }
}
</script>

<style scoped>
.logo{
    width: 10rem;
    height: 10rem;
}

.login{
    width: 25rem;
  height: 20rem;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

input{
    display: block;
    margin: auto;
    padding-left: 3rem;
    padding: 0.7rem;
    margin-bottom: 2rem;
    margin-top: 2rem;
    width: 20rem;
}
.login button{
    width: 5rem;
    width: 22rem;
    background-color: skyblue;
    padding: 0.5rem;
    border-radius: 0.5rem;
    cursor: pointer;
}
</style>