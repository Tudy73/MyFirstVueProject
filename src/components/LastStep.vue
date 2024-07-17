<script setup>
import {ref} from "vue";
import RecursiveTable from './RecursiveTable.vue'

const data =ref(null);
const emit = defineEmits(['next-page','increment']);
const props = defineProps({
  commonInfo: Number
})
async function fetchData(){
  try{
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    data.value = await response.json();
  }
  catch(e){
    console.error('The error is: ',e);
  }
}
function onEmit(){
  console.log(Object.values(data.value))
  emit('increment',Object.values(data.value).map(x => x['name']))
}
fetchData()
</script>

<template>
  <div>
    <button @click="onEmit">Share info</button>
    The shared information
    <RecursiveTable :data="[commonInfo]"/>
  </div>
  <button @click="$emit('next-page')">Go Back</button>
  <RecursiveTable :data="data"/>
</template>

<style scoped>
</style>