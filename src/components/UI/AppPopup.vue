<template>
  <transition name="popup-fade">
    <div
      v-if="value"
      @click.stop="hidePopup"
      class="popup"
    >
      <div
        @click.stop
        class="popup__content"
      >
        <div
          @click="hidePopup"
          class="popup__close"
        >&#x2715</div>

        <slot></slot>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    value: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hidePopup() {
      this.$emit('input', false)
    }
  }
}
</script>

<style scoped>
.popup {
  position: fixed;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;

  display: flex;
  justify-content: center;
  align-items: center;

  background: rgba(0, 0, 0, 0.5);
}

.popup__content {
  position: relative;

  padding: 20px;
  border-radius: 15px;

  background: white;
  box-shadow: 0 0 30px #2589FF;
}

.popup__close {
  position: absolute;
  top: 20px;
  right: 20px;

  cursor: pointer;

  color: #2589FF;
  transition: 0.4s ease;
}

.popup__close:hover {
  transform: scale(1.20);
}

.popup-fade-enter-active,
.popup-fade-leave-active {
  transition: 0.4s ease;
}
.popup-fade-enter,
.popup-fade-leave-to {
  opacity: 0;
}
</style>
