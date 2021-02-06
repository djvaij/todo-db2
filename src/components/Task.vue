<template>
  <div class="task">
    <input
      type="checkbox"
      class="task__checkbox"
      :checked="isCompleted"
      @click="toggleComplete(id)"
    >
    <span class="task__pseudo-checkbox pseudo-checkbox">
      <span class="pseudo-checkbox__icon">✓</span>
    </span>
    <div class="task__title">
      {{ title }} 
    </div>
    <div class="task__delete" @click="deleteTaksLocal">×</div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const { id, title, deleteTask } = defineProps({
  title: String,
  id: String|Number,
  deleteTask: Function,
  priority: Number,
  isCompleted: Boolean,
  toggleComplete: Function
})

const deleteTaksLocal = () => {
  deleteTask(id)
}

</script>

<style lang="scss" scoped>
.task {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-bottom: 10px;
  padding: 10px 12px;
  box-shadow: inset 0 0 3px rgba(#acacac, 0.7);
  border-radius: 3px;
  animation: show 0.5s ease;
}

.task {
  &__title {
    margin-left: 10px;
    margin-right: auto;
  }

  &__checkbox {
    cursor: pointer;
    width: 25px;
    height: 25px;
    border-radius: 50%;
    opacity: 0;
  }

  &__pseudo-checkbox {
    pointer-events: none;
    left: 16px;
    position: absolute;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 25px;
    height: 25px;
    border: 1px solid rgba(#acacac, 0.7);
    border-radius: 3px;
    transition: all 0.5s ease-out;
  }

  &__pseudo-checkbox .pseudo-checkbox__icon {
    position: relative;
    top: 5px;
    left: 2px;
    // display: none;
    opacity: 0;
    font-size: 20px;
    color: #42b983;
    transition: all 0.8s ease-out;
    animation: checkbox-out 0.5s ease;
  }

  &__checkbox:checked + &__pseudo-checkbox {
    border: 1px solid rgba(#42b983, 0.7);
  }

  &__checkbox:checked + &__pseudo-checkbox .pseudo-checkbox__icon {
    // display: inline;
    top: -8px;
    left: 2px;
    opacity: 1;
    animation: checkbox-in 0.5s ease;
    transition: opacity 0s ease-out;
    transform: scale(2);
  }

  &__checkbox:checked ~ &__title {
    color: gray;
    text-decoration: line-through;
  }

  &__delete {
    position: relative;
    z-index: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 25px;
    height: 25px;
    margin-left: auto;
    margin-right: 0;
    font-size: 20px;;
    cursor: pointer;

    &::before {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 0;
      height: 0;
      content: '';
      display: block;
      border-radius: 50%;
      background: rgba(#acacac, 0.3);
      transition: all 0.2s;
      transform: translate(-50%, -50%);
      z-index: -1;
    }

    &:hover {
      color: lightcoral;
    }

    &:hover::before {
      width: 100%;
      height: 100%;
    }
  }
}


@keyframes show {
  0% {
    transform: scale(0.5);
  }
  100% {
    transform: scale(1);
  }
}

@keyframes checkbox-in {
  0% {
    transform: scale(0.5);
  }
  25% {
    transform: scale(2);
  }
  75% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(2);
  }
}

@keyframes checkbox-out {
  0% {
    transform: scale(2);
  }
  100% {
    transform: scale(0.5);
  }
}

</style>