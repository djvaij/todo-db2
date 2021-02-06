<template>
  <div class="viewport">
    <div class="global-container">
      <Header
        :filters="filters"
        :filtersConst="filtersConst"
        :updateOrder="updateOrder"
        :changeStatusFilter="changeStatusFilter"
        :searchUpdate="searchUpdate"
      />
      <TodoList
        :todosList="todosList"
        :addTask="addTask"
        :deleteTaks="deleteTaks"
        :filters="filters"
        :filtersConst="filtersConst"
        :toggleComplete="toggleComplete"
        :search="search"
      />
    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import TodoList from './components/TodoList.vue'

import { defineProps, reactive, ref } from 'vue'

defineProps({
  msg: String
})

const filtersConst = {}

const filtersArray = [
  'ALL',
  'DONE',
  'UNDONE',
  'ASC',
  'DESC',
  'PRIOR',
]

filtersArray.forEach((element, index) => {
  Object.defineProperty( filtersConst, element, {
    value: index + 1,
    enumerable: false,
  });
})

function saveToLocalStorage(key, data) {
  window.localStorage.setItem(key, JSON.stringify(data))
}

function loadFromLocalStorage(key) {
  return JSON.parse(window.localStorage.getItem(key))
}

const defaultDemoTasks = [
  {
    id: 123,
    title: 'Leave email adress',
    isCompleted: true,
    timestamp: Date.now() + 1,
    priority: 5,
  },
  {
    id: 321,
    title: 'Wait for a test task',
    isCompleted: true,
    timestamp: Date.now() + 2,
    priority: 2,
  },
  {
    id: 456,
    title: 'Choose frontend framework',
    isCompleted: true,
    timestamp: Date.now() + 3,
    priority: 4,
  },
  {
    id: 789,
    title: 'Start develop app',
    isCompleted: true,
    timestamp: Date.now() + 4,
    priority: 1,
  },
  {
    id: 978,
    title: 'Send task to checking',
    isCompleted: true,
    timestamp: Date.now() + 5,
    priority: 3,
  },
  {
    id: 654,
    title: 'Wait for an answer',
    isCompleted: false,
    timestamp: Date.now() + 6,
    priority: 6,
  },
]

const defaultFilters = {
  status: filtersConst.ALL,
  order: filtersConst.DESC,
}

let todosFromLocalStorage = loadFromLocalStorage('todosList') || defaultDemoTasks
let filtersFromLocalStorage = loadFromLocalStorage('filters') || defaultFilters

let { todosList, filters } = reactive({
  todosList: [...todosFromLocalStorage],
  filters: filtersFromLocalStorage,
})

let search = reactive({
  searchText: ''
})

saveToLocalStorage('todosList', todosList)
saveToLocalStorage('filters', filters)

function uuidv4() {
  return 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
    var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
    return v.toString(16);
  });
}

const updateOrder = (order) => {
  filters.order = order
  sortBy(order)
  saveToLocalStorage('filters', filters)
}

const sortBy = (order) => {
  order = order || filters.order
  todosList.forEach((el) => {
    el.show = false
  })
  switch(order) {
    case filtersConst.ASC: {
      todosList = todosList.sort((a, b) => a.timestamp - b.timestamp)
      break
    }
    case filtersConst.DESC: {
      todosList = todosList.sort((a, b) => b.timestamp - a.timestamp)
      break
    }
    case filtersConst.PRIOR: {
      todosList = todosList.sort((a, b) => a.priority - b.priority)
      break
    }
  }
}

sortBy(filters.order)
saveToLocalStorage('filters', filters)

const addTask = (text) => {
  let newTaks = {
    id: uuidv4(),
    title: text,
    isCompleted: false,
    show: true,
    timestamp: Date.now(),
  }

  if (filters.order === filtersConst.DESC) {
    todosList.unshift(newTaks)
  }
  else if (filters.order === filtersConst.ASC) {
    todosList.push(newTaks)
  }
  else {
    todosList.push(newTaks)
  }
  window.scrollTo(0, document.querySelector("body").scrollHeight + 100)
  saveToLocalStorage('todosList', todosList)
}

const deleteTaks = (id) => {
  const deleteIndex = todosList.findIndex((el) => el.id === id)
  todosList.splice(deleteIndex, 1)
  saveToLocalStorage('todosList', todosList)
}

const changeStatusFilter = (status) => {
  todosList.forEach((el) => {
    el.show = false
  })
  filters.status = status
  saveToLocalStorage('filters', filters)
}

const toggleComplete = (id) => {
  todosList.forEach((el) => {
    if (el.id === id) {
      el.isCompleted = !el.isCompleted
    }
  })
  saveToLocalStorage('todosList', todosList)
}

const searchUpdate = (text) => {
  search.searchText = text
}

</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html,
body {
  padding: 0;
  margin: 0;
  background: rgba(#222, 0.8);
}

body {
  padding-top: 20px;
  min-height: 100vh;
  color: #eee;
  overflow-y: scroll;

  &::before {
    content: '';
    position: fixed;
    z-index: -1;
    top: 0;
    left: 0;
    width: 100vw;
    height: 120%;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
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