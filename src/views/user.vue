<template>
    <h1>page user</h1>
    <div v-for="user in users" :key="user.id">
        {{ user.fullName }} | {{ user.age }} in {{ user.created_at }}
    </div>
</template>



<script setup>

import {onMounted, ref} from 'vue';
import axios from 'axios';
 const users = ref([]);

 const getAllUser= async () =>{
    try {
        const response = await axios.get('http://127.0.0.1:8000/api/clients')
        users.value = response.data.clients;
       
    } catch (error) {
        console.log(error)
    }

 }

 onMounted(async()=>{
   await getAllUser();
 })


</script>


<style>


</style>