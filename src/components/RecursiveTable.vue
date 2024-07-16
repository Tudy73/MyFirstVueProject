<script setup>

import {computed} from "vue";
const props = defineProps({
  data: Object
})
const fields = computed(()=>{
  return props.data? Object.keys(props.data[0]):[]
})
const keys = computed(()=>{
  return props.data? props.data:[]
})
</script>

<template>
  <table>
    <tr>
      <th v-for="field in fields">
        {{field}}
      </th>
    </tr>
    <tr v-for="(user,index) in keys" :key="index">
      <td v-for="value in user">
        <RecursiveTable v-if="typeof value ==='object'" :data="[value]" />
        <span v-else>{{value}} </span>
      </td>
    </tr>

  </table>
</template>

<style scoped>

table, th, td {
  border: 1px solid white;
  border-collapse: collapse;
}

th, td {
  background-color: #172b50;
}
table{
  width: 100%;
}
</style>