<template>
  <header class="header">
    <input type="text" class="header__input" placeholder="Пошук..." v-model="typeText">
    <button id="filter-btn" class="header__button" @click="openFillters"></button>
    <Filters
      v-show="isFiltersShow"
      :filters="filters"
      :filtersConst="filtersConst"
      :updateOrder="updateOrder"
      :changeStatusFilter="changeStatusFilter"
    />
  </header>
</template>

<script setup>
import Filters from './Filters.vue'
import { defineProps, reactive, ref, watch } from 'vue'

let { searchUpdate } = defineProps({
  msg: String,
  filters: Object,
  filtersConst: Object,
  updateOrder: Function,
  changeStatusFilter: Function,
  searchUpdate: Function,
})

let state = reactive({ count: 0 })

let typeText = ref('')

watch(typeText, (first, second) => {
  searchUpdate(typeText)
  // console.log(typeText.value);
})

let isFiltersShow = ref(false)

const openFillters = (e) => {
  e.stopPropagation()
  isFiltersShow.value = !isFiltersShow.value
}

window.document.addEventListener("click", (e) => {
  if (e.target.id !== 'filter-btn') {
    isFiltersShow.value = false
  }
}, true)

</script>

<style scoped lang="scss">
@import "../scss/_icons.scss";

.header {
  position: relative;
  display: flex;
  align-items: center;
  padding: 30px 20px 80px;
  background: rgba(#202020, 0.7);
  border-radius: 5px;
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
}

.header {
  &__input {
    width: 100%;
    padding: 5px 15px;
    border: 1px solid rgba(#acacac, 0.7);
    border-radius: 5px;
    font-size: 16px;
    color: #42b983;
    background: #252525;
    
    &:focus {
      // border: 1px solid #42b983;
      border: none;
      outline: none;
      box-shadow: inset 0 0 3px #42b983;
      animation: searchAnimation 2s ease;
    }

    &::placeholder {
      color: rgba(#acacac, 0.7);
    }
  }

  &__button {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    max-width: 45.2px;
    height: 45.2px;
    margin-left: 25px;
    padding: 10px 15px;
    // border: 1px solid #acacac;
    border: none;
    border-radius: 5px;
    color: #acacac;
    font-size: 32px;
    font-weight: bold;
    transition: all 0.3s;
    // background-color: #252525;
    background-color: transparent;
    background-image: url($settings-icon);
    background-size: 24px;
    background-position: center;
    background-repeat: no-repeat;
    cursor: pointer;

    &:hover {
      background-image: url($settings-icon-hover);
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

@keyframes searchAnimation {
  0% {
    box-shadow: inset 0 0 0px #42b983;
  }
  100% {
    box-shadow: inset 0 0 3px #42b983;
  }
}

a {
  color: #42b983;
}
</style>