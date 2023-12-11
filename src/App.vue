<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="flex flex-col">
  <header class="absolute left-0 top-0 z-50 ml-5 bg-white border-2 p-2">
    <!--<img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />-->
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView class="w-90% h-90%"/>
  </div>
</template>