<template>
  <div class="viewport">
    <div class="global-container">
      <Header />
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  // background: #eeeeee;
  background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
}

.viewport {
  // background: #eeeeee;
  background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
}

.global-container {
  margin: auto;
  width: 100%;
  max-width: 920px;
}
</style>