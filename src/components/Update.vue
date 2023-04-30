<template>
    <Header />
    <h3>Hello, Welcome to Update Restaurant Page</h3>
    <div class="update">
    <input type="text" v-model="restaurant.name" placeholder="Enter Name"/>
    <input type="text" v-model="restaurant.address" placeholder="Enter Address"/>
    <input type="text" v-model="restaurant.contact" placeholder="Enter Contact"/>
    <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
    <p><router-link to="/">Back</router-link></p>
    </div>
    </template>
    
    <script>
    import axios from 'axios';
    import Header from '../components/Header.vue';
    
    export default {
        name: "Update",
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
        // For Update the Restaurant data
        async updateRestaurant()
        {
            const result = await axios.put("http://localhost:3000/restaurants/"+this.$route.params.id,{
                name:this.restaurant.name,
                address: this.restaurant.address,
                contact:this.restaurant.contact,
            });
            if(result.status==200)
            {
                this.$router.push({name:"Home"});
            }
        }
    },
    
    async mounted()
        {
            let user = localStorage.getItem('user-info');
            if(!user)
            {
                this.$router.push({name:'SignUp'})
            }

            // Code write to fetch id of restaurants
            let result =await axios.get ("http://localhost:3000/restaurants/"+this.$route.params.id);
            // +this.$route.params.id
            // for prefilling the data when we update 
            this.restaurant= result.data 
            console.log(result)
        }
    }
    
    </script>
    
    <style scoped>
.update{
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
.update button{
    width: 5rem;
    width: 22rem;
    background-color: skyblue;
    padding: 0.5rem;
    border-radius: 0.5rem;
    cursor: pointer;
}

    </style>