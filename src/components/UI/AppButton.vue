<template>
  <button class="button">
    <slot></slot>
  </button>
</template>

<style scoped>
.button {
  padding: 10px 15px;

  cursor: pointer;
  background-color: #2589FF;
  font-size: 16px;
  color: #FFFFFF;
  border: none;
  border-radius: 9px;
  transition: 0.4s ease;
}

.button:hover {
  box-shadow: 0 0 10px #2589FF;
}
</style>
