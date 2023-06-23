<template>
  <div class="select-wrapper">
    <div class="select-placeholder">
      {{ placeholder }}
    </div>

    <select
      @change="$emit('input', $event.target.value)"
      class="select"
    >
      <option selected disabled value="">Выберите из списка</option>
      <option
        v-for="option in options"
        :key="option.id"
        :value="option.id"
      >
        {{ `${option.name} (${option.id})` }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ''
    },
    options: {
      type: Array,
      default: () => []
    },
    placeholder: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
.select-wrapper {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

.select-placeholder {
  flex: 0 0 80px;
}

.select {
  flex-grow: 1;
  padding: 10px 15px;
  margin-left: 15px;

  border: 2px solid #2589FF;
  border-radius: 10px;

  transition: 0.4s ease;
}

.select:focus {
  outline: none;
  box-shadow: 0 0 5px #2589FF;
}
</style>
