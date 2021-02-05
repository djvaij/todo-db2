<template>
  <div class="viewport">
    <div class="global-container">
      <Header />
      <TodoList />
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import TodoList from './components/TodoList.vue'
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html,
body {
  padding: 0;
  margin: 0;
  // background: #eeeeee;
  // background-image: linear-gradient(-45deg, #84fab0, #8fd3f4);
  // background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
  background: linear-gradient(-45deg, #23a6d5, #23d5ab);
  background-size: 400% 400%;
	animation: gradient 5s ease infinite;
}

body {
  min-height: calc(100vh - 20px);
}

.viewport {
  // background: #eeeeee;
  // background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
}

.global-container {
  width: 100%;
  max-width: 920px;
  margin: auto;
  padding: 0 15px;
}

@keyframes gradient {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}
</style>