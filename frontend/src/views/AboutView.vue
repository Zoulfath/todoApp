<template>
  <div class="about bg-white text-black rounded-2xl my-4">
    <main >
    <WelcomeItem class="item"/>
  </main>
  </div>
</template>

<script setup>
import WelcomeItem from '../components/WelcomeItem.vue'
</script>

<style>
main{
  background-color: white;
  color: black;
  max-height: 100vh;
}

</style>
