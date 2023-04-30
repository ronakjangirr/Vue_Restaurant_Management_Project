<template>
<Header />
<h3>Hello {{ name }}, Welcome to Add Restaurant Page</h3>
<div class="add">
    <input type="text" v-model="restaurant.name" placeholder="Enter Name"/>
    <input type="text" v-model="restaurant.address" placeholder="Enter Address"/>
    <input type="text" v-model="restaurant.contact" placeholder="Enter Contact"/>
    <button type="button" v-on:click="addRestaurant">Add Restaurant</button>
    <p><router-link to="/">Back</router-link></p>
</div>

</template>

<script>
import axios from 'axios';
import Header from '../components/Header.vue';

export default {
    name: "Add",
    components:{
        Header
    },
    
    data()
    {
    return{
        restaurant:{
            name:'',
            address:'',
            contact:''
        }
    }
    },

    methods:{
        async addRestaurant()
        {
            console.log(this.restaurant);
            const result = await axios.post("http://localhost:3000/restaurants",{
                name:this.restaurant.name,
                address: this.restaurant.address,
                contact:this.restaurant.contact,
            });
            if(result.status==201)
            {
                this.$router.push({name:"Home"});
            }
            console.log("result", result)
        }
    },


    mounted()
    {
        let user = localStorage.getItem('user-info');
        this.name= JSON.parse(user).name  // This is use to show user's name on beside welcome test

        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
    }
}

</script>

<style scoped>
.add{
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
.add button{
    width: 5rem;
    width: 22rem;
    background-color: skyblue;
    padding: 0.5rem;
    border-radius: 0.5rem;
    cursor: pointer;
}
</style>