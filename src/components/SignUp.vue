<template>
    <img class="logo" src="../assets/resto-logo.png"/>
<h3>Sign Up Page</h3>
<div class="register">
    <input type="text" v-model="name" placeholder="Enter Name"/>
    <input type="text" v-model="email" placeholder="Enter Email"/>
    <input type="password" v-model="password" placeholder="Enter Password"/>
    <button v-on:click="signUp">Sign Up</button>
    <p><router-link to="/login">Login</router-link></p>
</div>
</template>

<script>
import axios from 'axios';
export default {
    name: "SignUp",
    data()
    {
    return{
        name:'',
        email:'',
        password:''
    }
    },
    methods:{
    async signUp()
        {
            console.log("signUp", this.name, this.email, this.password)
            let result= await axios.post("http://localhost:3000/users",{
                email:this.email,
                name:this.name,
                password:this.password
            });
            console.log(result);
            if(result.status==201)
            {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                alert("Sign Up Done");
                this.$router.push({name:'Home'})
            }
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
</script>

<style scoped>
.logo{
    width: 10rem;
    height: 10rem;
}

.register{
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
.register button{
    width: 5rem;
    width: 22rem;
    background-color: skyblue;
    padding: 0.5rem;
    border-radius: 0.5rem;
    cursor: pointer;
}
</style>