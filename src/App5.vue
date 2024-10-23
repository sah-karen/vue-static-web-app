<script setup>
import User from './components/User.vue'
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
  

function deleteUser(index){
    users.value.splice(index,1)
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
<!-- Send props to user ':userEl="el"',  userEl can be any name, but in User.vue in "defineProps()" it must be the same too: "userEl" -->
  <User v-for="el, index in users" :key="index" :userEl="el"  :indexProp="index" :deleteUser="deleteUser"/>

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
