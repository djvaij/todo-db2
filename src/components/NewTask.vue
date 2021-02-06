<template>
  <div class="new-task">
    <input
      v-model="taskText"
      type="text"
      class="new-task__input"
      placeholder="Type your task here..."
      @keypress.enter="addNewTask"
    >
    <button class="new-task__add-btn" @click="addNewTask">+</button>
  </div>
</template>

<script setup="props">
import { defineProps, ref } from 'vue'

const props = defineProps({
  addTask: Function
})

let taskText = ref('')

const addNewTask = () => {
  if (taskText.value !== '') {
    props.addTask(taskText.value)
    taskText.value = ''
  }
}
</script>

<style lang="scss" scoped>
.new-task {
  display: flex;
  align-items: center;
  margin-bottom: 40px;

  &__input {
    width: 100%;
    padding: 5px 15px;
    border: none;
    border-bottom: 1px solid rgba(#acacac, 0.7);
    // border-radius: 3px;
    font-size: 16px;
    color: #42b983;
    // background: #202020;
    background: transparent;
    
    &:focus {
      border: none;
      border-bottom: 1px solid #42b983;
      outline: none;
    }

    &::placeholder {
      color: rgba(#acacac, 0.7);
    }
  }

  .new-task__input:focus ~ .new-task__add-btn {
    color: #42b983;
    box-shadow: inset 0 0 0px #42b983;
    animation: shadow 1s ease infinite;
  }

  &__add-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    max-width: 45.2px;
    height: 32px;
    margin-left: 25px;
    padding: 10px 15px;
    // border: none;
    // border: 1px solid #acacac;
    border: none;
    border-radius: 3px;
    color: #acacac;
    font-size: 32px;
    font-weight: bold;
    transition: all 0.3s;
    background-color: transparent;
    // background-image: url($settings-icon);
    background-size: 24px;
    background-position: center;
    background-repeat: no-repeat;
    cursor: pointer;

    &:hover {
      // background-image: url($settings-icon-hover);
      // border: 1px solid #42b983;
      color: #42b983;
      box-shadow: inset 0 0 0px #42b983;
      animation: shadow 1s ease infinite;
    }

    &:focus {
      outline: none;
    }
  }
}

@keyframes shadow {
  0% {
    box-shadow: inset 0 0 0px #42b983;
  }
  50% {
    box-shadow: inset 0 0 3px #42b983;
  }
  100% {
    box-shadow: inset 0 0 0px #42b983;
  }
}
</style>