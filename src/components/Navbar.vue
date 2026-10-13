<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { withBase } from '../utils/utils'



onMounted(() => {
  
});

onUnmounted(() => {

});
</script>

<template>
  <div id="navbar" class="absolute top-0 left-0 p-5 w-full h-[85px] z-50 flex items-center">
    <a :href="withBase('/')" class="inline-block h-full">
        <img :src="withBase('/auroratrustaward_logo.svg')" class="h-full w-auto" alt="logo">
    </a>
  </div>
</template>

<style scoped>
    
</style>