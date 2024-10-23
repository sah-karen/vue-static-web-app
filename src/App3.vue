<script setup>
import {ref} from 'vue'
const info = ref('Title!1')
const someInfo = ref("Anonce of nsessages")

const change = (par='New Text') => {
  someInfo.value = par // change ref value
  info.value = "Some Text"
}

</script>

<template>
  <h3> {{ info}}</h3>
  <p> {{ someInfo }}</p>
  <button type="button" @click="change('Value')">Change</button>
</template>
 
<style scoped>
h3{
  font-weight: lighter ;
}
p{
  color: rgb(136, 65, 65);
}

</style>
