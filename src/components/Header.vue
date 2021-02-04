<template>
  <header>
    s
  </header>
</template>

<script setup>
import { defineProps, reactive } from 'vue'

defineProps({
  msg: String
})

const state = reactive({ count: 0 })
</script>

<style scoped lang="scss">
a {
  color: #42b983;
}
</style>