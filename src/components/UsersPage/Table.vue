<template>
  <div class="users-table">
    <div class="users-table__row">
      <div
        class="users-table__ceil users-table__ceil--clickable"
        @click="sortUsers(sortedUsers, 'name')"
      >Имя</div>
      <div
        class="users-table__ceil users-table__ceil--clickable"
        @click="sortUsers(sortedUsers, 'phone')"
      >Телефон</div>
    </div>

    <table-item
      v-for="user in sortedUsers"
      :key="user.id"
      :user="user"
    />
  </div>
</template>

<script>
import TableItem from "./TableItem.vue";

export default {
  components: {
    TableItem
  },
  props: {
    users: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      sortedUsers: [],
      activeSort: ''
    }
  },
  watch: {
    users(newValue) {
      this.sortedUsers = [...newValue];

      if (this.activeSort) {
        this.sortUsers(this.sortedUsers, this.activeSort);
      }
    }
  },
  methods: {
    sortUsers(users, label) {
      this.activeSort = label;

      users.sort((a, b) => {
        if ([a[label], b[label]].some(e => typeof e === 'string')) {
          return a[label].localeCompare(b[label]);
        } else {
          const phone1 = Number(a[label].substring(1).replace(/\s/g, ""));
          const phone2 = Number(b[label].substring(1).replace(/\s/g, ""));
          return phone1 - phone2;
        }
      })

      users.forEach((user) => {
        if (user.children) {
          this.sortUsers(user.children, label);
        }
      })
    }
  }
}
</script>

<style scoped>
.users-table {
  display: grid;
  grid-gap: 3px;
}

/deep/ .users-table__row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-column-gap: 3px;
}

/deep/ .users-table__ceil {
  padding: 8px 10px 8px 35px;
  border: 3px solid #2589FF;
}

.users-table__ceil--clickable {
  background-color: #2589FF;
  color: #FFFFFF;
  cursor: pointer;
}
</style>
