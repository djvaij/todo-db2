<template>
  <div class="new-task">
    <input type="text" class="new-task__input">
    <button class="new-task__add-btn">+</button>
  </div>
</template>

<style lang="scss" scoped>
.new-task {
  display: flex;
  align-items: center;
  background: #f7f7f7;
  border-radius: 5px;

  &__input {
    width: 100%;
    padding: 10px 15px;
    border: 1px solid #acacac;
    border-radius: 5px;
    font-size: 20px;
    color: #42b983;
    
    &:focus {
      border: 1px solid #42b983;
      outline: none;
    }

    &::placeholder {
      color: rgba(#acacac, 0.7);
    }
  }

  &__add-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    max-width: 45.2px;
    height: 45.2px;
    margin-left: 25px;
    padding: 10px 15px;
    border: 1px solid #acacac;
    border-radius: 5px;
    color: #acacac;
    font-size: 32px;
    font-weight: bold;
    transition: all 0.3s;
    background-color: white;
    // background-image: url($settings-icon);
    background-size: 24px;
    background-position: center;
    background-repeat: no-repeat;
    cursor: pointer;

    &:hover {
      // background-image: url($settings-icon-hover);
      border: 1px solid #42b983;
      color: #42b983;
      box-shadow: inset 0 0 0px #42b983;
      animation: shadow 1s ease infinite;
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