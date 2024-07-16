<script setup>
import { ref} from 'vue'
import FirstStep from './components/FirstStep.vue'
import LastStep from './components/LastStep.vue'
const currentPath = ref(FirstStep)
</script>

<template>
  <main>
    <component :is="currentPath"
    @next-page="()=>{currentPath=LastStep}"/>
  </main>
</template>