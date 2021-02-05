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
  background: rgba(#222, 0.8);
}

body {
  padding-top: 20px;
  min-height: 100vh;
  color: #eee;

  &::before {
    content: '';
    position: fixed;
    z-index: -1;
    top: 0;
    left: 0;
    width: 100vw;
    height: 120%;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    // background: linear-gradient(-45deg, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradient 5s ease infinite;
  }
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