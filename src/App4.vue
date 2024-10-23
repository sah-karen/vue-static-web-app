<script setup>
import {ref} from 'vue'
const username=ref('')
const userpass=ref('')
const useremail=ref('')
const error=ref('')
const users = ref([])

const insertData = (par) => {
  username.value = par 
}

const sendData = ()=>{
    if (username.value == ''){
      error.value = 'Name is not entered';
      return;
    }else if(userpass.value == '') {
      error.value = 'Password is not entered';
      return;
    }else if(useremail.value == '') {
      error.value = 'Email is not entered';
      return;
    }
    error.value = ''
     users.value.push({
        name: username.value,
        pass: userpass.value,
        email: useremail.value
      })
}
  
</script>

<template>
  <input type="text" @input="insertData($event.target.value)" placeholder="Name">
  <input type="password" v-model="userpass" placeholder="Password">
  <input type="email" v-model="useremail" placeholder="Email">
  <p className="error">{{ error }}</p>
  <button @click="sendData()">Send</button>

  <div v-if="users.length == 0" className="user">
      There is no users
  </div>
  <div v-else-if="users.length == 1" className="user">
      Users has 1 element
  </div>
  <div v-else className="user">
      Users has more than 1 element
  </div>

  <div v-for="el, index in users" :key="index" className="user">
      <h3>{{ el.name }}</h3>
      <p>{{el.email}} - <b>{{ el.pass }}</b></p>
  </div>
  <!-- <p>{{ users }}</p> -->
  <!-- <p>{{ username }}</p>
  <p>{{ userpass }}</p>
  <p>{{ useremail }}</p> -->
</template>
 
<style scoped>
.user{
  width: 500px;
  margin-top: 20px;
  border: 1px solid silver;
  background: #e3e3e3;
  color: #222;
  padding: 20px;
  border-radius: 5px;
}
</style>
