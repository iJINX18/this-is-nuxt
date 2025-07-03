<template>
  <div class="page-container">
    <Header />
    <NuxtPage />
    <Footer class=" page-content"/>
  </div>
</template>
<style scoped>

.page-container {
  display: flex; 
  flex-direction: column;
  min-height: 100vh; 
}

.page-content {
  flex: 1;
} 
</style>