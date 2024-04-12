<script setup>
import { RouterLink, RouterView } from 'vue-router'
import IconDocumentation from './components/icons/IconDocumentation.vue';
import IconSupport from './components/icons/IconSupport.vue';
</script>

<template>
  <!-- <header class="mt-4 max-h-full">

    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="40" height="40" />

    <div >
      <nav>

        <div class="f-nav flex ">
          <IconDocumentation class="IconDocumentation"/>
          <RouterLink to="/" >
          Home
          </RouterLink>
        </div>

        <div class="s-nav flex">
          <IconSupport class="IconSupport"/>
          <RouterLink to="/about">
          About
        </RouterLink>
        </div>

      </nav>
    </div>
  </header> -->

  <RouterView class="router" />
</template>

<style>
nav{
  color: white;
  font-size: 20px;
}

.IconDocumentation {
  margin-right: 15px;
}

.IconSupport{
  margin-right: 15px;
}

header{
  max-width: 100vh;
}

.f-nav {
  display: flex;
  align-items: center;
}
.s-nav {
  display: flex;
  align-items: center;
}

</style>
