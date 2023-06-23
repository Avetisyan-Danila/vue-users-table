<template>
  <div class="user-page">
    <app-button
      @click.native="showForm"
      class="user-page__btn"
    >
      Добавить
    </app-button>

    <user-table :users="users"/>

    <app-popup
      v-model="isFormVisible"
      class="user-page__popup"
    >
      <user-form
        :users="users"
        @submit="handleSubmitUserForm"
      />
    </app-popup>
  </div>
</template>

<script>
import UserTable from './Table.vue';
import UserForm from './Form.vue';
import AppPopup from "../UI/AppPopup.vue";
import AppButton from "../UI/AppButton.vue";
import mockUsers from '../../mocks/users.json'

export default {
  components: {
    UserTable,
    UserForm,
    AppPopup,
    AppButton
  },
  data() {
    return {
      users: [],
      isFormVisible: false
    }
  },
  watch: {
    users: {
      handler: function (newValue) {
        localStorage.setItem('users', JSON.stringify(newValue));
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.getItem('users')) {
      this.users = JSON.parse(localStorage.getItem('users'));
    } else {
      this.users = mockUsers;
    }
  },
  methods: {
    findChiefInUsers(users, chiefId) {
      let chief = null;

      (function search(users) {
        for (let user of users) {
          if (user.id === chiefId) {
            chief = user;
          } else if (user.children) {
            search(user.children);
          }
        }
      })(users);

      return chief;
    },
    findChiefParent(users, chief) {
      let parent = null;

      if (users.includes(chief)) {
        parent = users;
      } else {
        (function search(users) {
          for (let user of users) {
            if (user.children && user.children.includes(chief)) {
              parent = user;
            } else if (user.children) {
              search(user.children);
            }
          }
        })(users);
      }

      return parent;
    },
    handleSubmitUserForm(newUser) {
      this.hideForm();

      const userData = {
        id: String(Date.now()),
        name: newUser.name,
        phone: newUser.phone
      };

      if (!newUser.chiefId) {
        this.users.push(userData);
      } else {
        const chief = this.findChiefInUsers(this.users, newUser.chiefId);
        const chiefParent = this.findChiefParent(this.users, chief);

        if (chief && chief.children) {
          chief.children.push(userData);
        } else {
          if (chiefParent.children) {
            chiefParent.children = chiefParent.children.map((child) => {
              if (child.id === chief.id) {
                return Object.assign({children: [userData]}, child);
              } else {
                return child;
              }
            });
          } else {
            const chiefIndex = chiefParent.findIndex((user) => user.id === chief.id);
            const newChief = Object.assign({children: [userData]}, chiefParent[chiefIndex]);
            chiefParent.splice(chiefIndex, 1, newChief);
          }
        }
      }
    },
    showForm() {
      this.isFormVisible = true;
    },
    hideForm() {
      this.isFormVisible = false;
    }
  }
}
</script>

<style scoped>
.user-page {
  max-width: 700px;
  margin: 0 auto;
  padding-top: 40px;
}

.user-page__btn {
  margin-bottom: 20px;
}

/deep/ .user-page__popup .popup__content {
  max-width: 450px;
  width: 100%;
}
</style>
