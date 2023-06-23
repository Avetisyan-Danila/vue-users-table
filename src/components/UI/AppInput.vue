<template>
  <div
    class="input-wrapper"
    :class="{ 'input-wrapper--required': required }"
  >
    <div class="input-placeholder">
      {{ placeholder }}
    </div>

    <input
      :value="value"
      @input="$emit('input', $event.target.value)"
      :type="type"
      class="input"
    >
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    },
    required: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
.input-wrapper {
  position: relative;

  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

.input-wrapper--required:before {
  content: '*';
  position: absolute;
  top: 3px;
  left: -8px;
  color: red;
}

.input-placeholder {
  flex: 0 0 80px;
}

.input {
  flex-grow: 1;
  padding: 10px 15px;
  margin-left: 15px;

  border: 2px solid #2589FF;
  border-radius: 10px;

  transition: 0.4s ease;
}

.input:focus {
  outline: none;
  box-shadow: 0 0 5px #2589FF;
}
</style>
