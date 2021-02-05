<template>
  <div class="todo-list">
    <new-task />
    <div v-show="todoList.length < 1" class="todo-list__no-todos no-todos">
      Please add your first task...
    </div>
    <div v-show="todoList.length > 0" class="todo-list__list">
      <div class="task" v-for="item in todoList" :key="item.id">
        {{ item.title }}
      </div>
    </div>
  </div>
</template>

<script setup>
import NewTask from './NewTask.vue'
import { defineProps, reactive } from 'vue'

defineProps({
  todoList: Array,
  msg: String,
})

const state = reactive({
  todoList: [],
  msg: "",
})

let { todoList } = state

todoList.push({
  id: 1,
  title: "First task",
  complated: false,
})

todoList.push({
  id: 2,
  title: "Seccond task",
  complated: false,
})

console.log(todoList)

</script>

<style lang="scss" scoped>
.todo-list {
  display: flex;
  flex-direction: column;
  // margin-top: 20px;
  padding: 15px 20px;
  background: rgba(#202020, 0.7);
  border-radius: 5px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}

.no-todos {
  width: 100%;
  padding: 10px 15px;
  border-radius: 5px;
  font-size: 20px;
  color: #42b983;
}
</style>