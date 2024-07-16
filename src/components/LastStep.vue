<script setup>
import {ref} from "vue";
import RecursiveTable from './RecursiveTable.vue'

const data =ref(null);
async function fetchData(){
  try{
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    data.value = await response.json();
  }
  catch(e){
    console.error('The error is: ',e);
  }
}
fetchData()
</script>

<template>
<RecursiveTable :data="data"/>
</template>

<style scoped>
</style>