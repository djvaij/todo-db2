<template>
  <div class="todo-list">
    <NewTask :addTask="props.addTask"/>
    <div class="todo-list__list">
      <transition-group name="list" tag="div">
        <Task
          v-for="item in filteredList"
          :key="item.id"
          :title="item.title"
          v-show="item.show"
          :id="item.id"
          :deleteTask="props.deleteTaks"
          :priority="item.priority"
          :isCompleted="item.isCompleted"
          :toggleComplete="toggleComplete"
        />
      </transition-group>
    </div>
  </div>
</template>

<script setup="props, { emit }">
import NewTask from './NewTask.vue'
import Task from './Task.vue'
import { defineProps, reactive, watch, ref } from 'vue'

const props = defineProps({
  todosList: Array,
  addTask: Function,
  deleteTaks: Function,
  filters: Object,
  filtersConst: Object,
  toggleComplete: Function,
  search: Object
})

let { todosList, filters, filtersConst, search } = props

let counter = 0

let filteredList = ref([...todosList])

function update() {
  if (filters.status === filtersConst.DONE) {
    filteredList.value = [...todosList]
      .filter((el) => el.isCompleted)
      .filter((el) =>
        el.title.toLowerCase().includes(search.searchText.toLowerCase()))
  }
  else if (filters.status === filtersConst.UNDONE) {
    filteredList.value = [...todosList]
      .filter((el) => !el.isCompleted)
      .filter((el) =>
        el.title.toLowerCase().includes(search.searchText.toLowerCase()))
  } else {
    filteredList.value = [...todosList]
      .filter((el) =>
        el.title.toLowerCase().includes(search.searchText.toLowerCase()))
  }
}

watch(props.search, (first, second) => {
  update()
})

watch(props.filters, (first, second) => {
  counter = 0
  update()
  showElements()
})

watch(props.todosList, (first, second) => {
  counter = 0
  update()
  showElements()
})

function showElements() {
  if (counter < todosList.length) {
    setTimeout(() => {
      todosList[counter].show = true
      counter++
      showElements()
    }, 100)
  } else {
    counter = 0
  }
}

showElements()

</script>

<style lang="scss" scoped>
.todo-list {
  display: flex;
  flex-direction: column;
  min-height: calc(100vh - 200px);
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

.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  margin-top: -60px;
  transform: scale(0.5) translateY(60px);
}
</style>