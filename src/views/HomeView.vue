<template>
  <h1>page user</h1>
  <input type="text" v-model="userfullName" @keyup.enter="adduserFullname()">
  <div v-for="user in users" :key="user.id">
      {{ user.fullName }} 
  </div>
</template>



<script setup>
import {ref,onMounted} from 'vue';
import axios from 'axios';
const userfullName = ref('');
const users = ref([]);

const getAllUser= async () =>{
  try {
      const response = await axios.get('http://127.0.0.1:8000/api/clients')
      users.value = response.data.clients;
     
  } catch (error) {
      console.log(error)
  }

}

const adduserFullname= async () =>{
  try{
    const user = {
      'fullName':userfullName.value,
      'age':20
    }
    const result = await axios.post('http://127.0.0.1:8000/api/clients',user)
    users.value.push(result.data.client)
    userfullName.value=''

  }catch(error){
    console.log(error)
  }

}

onMounted(async()=>{
 await getAllUser();
})


</script>


<style>


</style>