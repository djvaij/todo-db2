<template>
  <div class="filters">
    <div class="filters__group">
      Show:
      <div class="filter-item">
        <input
          type="radio"
          name="status"
          id="status-1"
          :checked="filters.status === filtersConst.ALL"
          @click="localUpdate(filtersConst.ALL)"
        >
        <label for="status-1">All</label>
      </div>
      <div class="filter-item">
        <input
          type="radio"
          name="status"
          id="status-2"
          :checked="filters.status === filtersConst.DONE"
          @click="localUpdate(filtersConst.DONE)"
        >
        <label for="status-2">Done</label>
      </div>
      <div class="filter-item">
        <input
          type="radio"
          name="status"
          id="status-3"
          :checked="filters.status === filtersConst.UNDONE"
          @click="localUpdate(filtersConst.UNDONE)"
        >
        <label for="status-3">Undone</label>
      </div>
    </div>

    <hr>

    <div class="filters__group">
      Sort by:
      <div class="filter-item">
        <input
          type="radio"
          name="order"
          id="order-1"
          :checked="filters.order === filtersConst.ASC"
          @click="localSort(filtersConst.ASC)"
        >
        <label for="order-1">Ascending</label>
      </div>
      <div class="filter-item">
        <input
          type="radio"
          name="order"
          id="order-2"
          :checked="filters.order === filtersConst.DESC"
          @click="localSort(filtersConst.DESC)"
        >
        <label for="order-2">Descending</label>
      </div>
      <!-- <div class="filter-item">
        <input
          type="radio"
          name="order"
          id="order-3"
          :checked="filters.order === filtersConst.PRIOR"
          @click="localSort(filtersConst.PRIOR)"
        >
        <label for="order-3">Priority</label>
      </div> -->

    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const { updateOrder, changeStatusFilter } = defineProps({
  filters: Object,
  filtersConst: Object,
  updateOrder: Function,
  changeStatusFilter: Function,
})

const localUpdate = (status) => {
  changeStatusFilter(status)
}

const localSort = (order) => {
  updateOrder(order)
}
</script>

<style lang="scss" scoped>
.filters {
  position: absolute;
  z-index: 1;
  top: 80px;
  right: 20px;
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  width: 150px;
  padding: 10px 20px;
  border: 1px solid rgba(#acacac, 0.7);
  border-radius: 5px;
  background: #252525;
  font-size: 16px;
}

hr {
  width: 100%;
}
</style>