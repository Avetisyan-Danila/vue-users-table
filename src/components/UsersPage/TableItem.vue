<template>
  <div
    class="users-table__row"
    :class="{ 'users-table__row--has-children':  userHasChildren }"
  >
    <div
      v-if="userHasChildren"
      @click="isOpened = !isOpened"
      class="users-table__open"
      :class="{ 'users-table__open--active': isOpened }"
    >
      {{ isOpened ? '-' : '+' }}
    </div>

    <div class="users-table__ceil">{{ `${user.name} (id: ${user.id})` }}</div>
    <div class="users-table__ceil">{{ user.phone }}</div>

    <div
      v-if="userHasChildren"
      class="users-table__child"
      :class="{ 'users-table__child--opened': isOpened }"
    >
      <table-item
        v-for="user in user.children"
        :key="user.id"
        :user="user"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "TableItem",
  props: {
    user: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      isOpened: false
    }
  },
  computed: {
    userHasChildren() {
      return this.user.children && this.user.children.length > 0;
    }
  }
}
</script>

<style scoped>
.users-table__row--has-children {
  position: relative;
}

.users-table__open {
  position: absolute;
  top: 20px;
  transform: translateY(-50%);
  left: 10px;
  cursor: pointer;
  font-size: 20px;
  font-weight: 700;
}

.users-table__open--active {
  left: 13px;
}

.users-table__child {
  display: grid;
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-gap: 3px;

  opacity: 0;
  height: 0;
  overflow: hidden;
  transition: 0.4s ease;
}

.users-table__child--opened {
  height: auto;
  opacity: 1;
  transform: translateY(3px);
  margin-bottom: 3px;
}

.users-table__child > .users-table__row {
  width: calc(100% - 20px);
  margin-left: calc(100% - (100% - 10px));
}
</style>
