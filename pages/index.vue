<template>
  <h1>Home Page</h1>
    <button><NuxtLink to="/TaskTracker" class="nuxt-link">Go to TaskTracker</NuxtLink></button>
    <button><NuxtLink to="/about" class="nuxt-link">Go to About</NuxtLink></button><br/>


</template>

<script setup>

</script>

<style scoped>

button{
  background-color: gray;
  width: 100px
}

.nuxt-link {
  font-weight: bold;
  color: white;
  text-decoration: none;
}

</style>