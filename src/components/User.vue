<template>
    <div className="user">
        <button @click="deleteUser(indexProp)">Delete</button>
        <h3>{{ userEl.name }}</h3>
        <p>{{userEl.email}} - <b>{{ userEl.pass }}</b></p>
    </div>
</template>

<script setup>
defineProps(
     { userEl: {
         type: Object,
         required: true
        },
        indexProp: {
            type: Number,
            required: true
        },
        deleteUser:{
            type: Function,
            required: true
        }
    }
)

</script>

<style scoped>
button{
  border: 0;
  border-radius: 5px;
  outline: none;
  padding: 10px 15px;
  background: #d66c75;
  color: #711629;
  font-weight: bold;
  cursor: pointer;
  transition: transform 500ms ease;
  float: right;
}

button:hover{
    transform: translateY(-5px);
}
</style>