<template>
 <input v-model="searchKey" placeholder="Filter Name" v-on:keyup="filterTable" />
 {{searchKey}}
<div v-if='users'>

  <ul v-for='user in users' :key='user.id'>
    <li>{{user.name}}</li>
  </ul>
</div>
</template>


<script>
import axios from 'axios';
export default {
  name: 'App',
  async mounted(){
     this.usersStore = (await axios.get('https://jsonplaceholder.typicode.com/users')).data;
     this.users = this.usersStore;
  },
  data() {
    return { 
      users: false,
      usersStore: false,
      searchKey:'' }
  },
  methods: {
    filterTable(){
     if(this.searchKey == ''){
     this.users = this.usersStore
     }
     else{
       let filUser = []
       this.usersStore.forEach(u => {
         const name = u.name.toLowerCase();
         if(name.includes(this.searchKey.toLowerCase()))
          filUser.push(u);
       })
        this.users = filUser;
        }
       
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
