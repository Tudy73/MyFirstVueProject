<script setup>
import {reactive, ref} from 'vue'
import FirstStep from './components/FirstStep.vue'
import LastStep from './components/LastStep.vue'
const pages = reactive([FirstStep,LastStep])
const currentIndex = ref(0);
const common = ref(0);
function setCommonData(value){
  common.value = value;
}
</script>

<template>
  <main>
    <component :is="pages[currentIndex]"
    @next-page="()=>{currentIndex=1-currentIndex}"
    :commonInfo = "common"
    @increment="setCommonData"/>
  </main>
</template>