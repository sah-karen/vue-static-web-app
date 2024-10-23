<script setup>
import User from './components/User.vue'
import axios from 'axios'
import {ref, computed} from 'vue'

const city=ref('')
const error=ref('')
const info=ref(null)


const cityName=computed(()=>"<" + city.value + ">")
const showTemp=computed(()=>"Temperature: " + info.value.main.temp + " C")
const showFeelsLike=computed(()=>"Feels like: " + info.value.main.feels_like + " C")
const showMinTemp=computed(()=>"Min temperature: " + info.value.main.temp_min + " C")
const showMaxTemp=computed(()=>"Max temperature: " + info.value.main.temp_max + " C")



function getWeater(){
  if(city.value.trim().length < 2){
    error.value = "City name's lenght must be more one symbol ;)" 
    return false
  }
  error.value = ""
  // weather?q=Yerevan  weather?q=${city.value}
  axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city.value}&units=metric&appid=3c720744fdffed8eba77cfbfa0911a74`)
        .then(res=> (info.value = res.data))

}
</script>

<template>
    <div class="wrapper">
        <h1> Wheather application </h1>
        <p>Know wheather in {{ city  == "" ? "your city" : cityName}}</p>
        <!-- <input type="text" @input="city=$event.target.value" placeholder="Input town"> -->
        <input type="text" v-model="city" placeholder="Input city">
        <button v-if="city != ''"  @click="getWeater()">Get weather</button>
        <button v-else disabled>Input city value</button>
        <p class="error">{{ error }}</p>
        <div v-if="info != null">
          <p>{{ showTemp }}</p>
          <p>{{ showFeelsLike }}</p>
          <p>{{ showMinTemp }}</p>
          <p>{{ showMaxTemp }}</p>
        </div>  
    </div>
</template>
 
<style scoped>
.error {
  color: #d03939;
}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: #fff
}
.wrapper h1{
    margin-top: 50px;
}
.wrapper p{
    margin-top: 20px;
}
.wrapper input{
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}
 .wrapper input:focus {
    border-bottom-color: #6e2d7d;
 }

 .wrapper button:disabled{
  cursor: not-allowed;
  background: #6e2d7d;
 }

 .wrapper button{
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 20px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}

</style>
