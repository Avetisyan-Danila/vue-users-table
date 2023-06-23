<template>
  <form
    class="form"
    action=""
    @submit.prevent="handleSubmitForm"
  >
    <h3 class="form__title">Добавление пользователя</h3>

    <app-input
      v-model.trim="formFields.name"
      placeholder="Имя"
      required
    />

    <app-input
      v-model.trim="formFields.phone"
      placeholder="Телефон"
      type="tel"
      required
    />

    <app-select
      v-if="users.length"
      v-model="formFields.chiefId"
      :options="sortedSelectOptions"
      placeholder="Начальник"
    />

    <div
      v-show="!isFormValid"
      class="form__error-message"
    >
      Заполните обязательные поля!
    </div>

    <app-button>Сохранить</app-button>
  </form>
</template>

<script>
import AppInput from "../UI/AppInput.vue";
import AppButton from "../UI/AppButton.vue";
import AppSelect from "../UI/AppSelect.vue";

export default {
  components: {
    AppButton,
    AppInput,
    AppSelect
  },
  props: {
    users: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      formFields: {
        name: '',
        phone: '',
        chiefId: ''
      },
      selectOptions: [],
      isFormValid: true
    }
  },
  computed: {
    sortedSelectOptions() {
      return this.selectOptions.sort((a, b) => {
        if (a.name < b.name) return -1;
        if (a.name > b.name) return 1;
        return 0;
      })
    }
  },
  watch: {
    formFields: {
      handler: function () {
        this.isFormValid = true;
      },
      deep: true
    }
  },
  mounted() {
    this.selectOptions = this.setSelectOptions(this.users);
  },
  methods: {
    setSelectOptions(users) {
      const a = [];

      (function addOption(users) {
        for (let user of users) {
          a.push({
            id: user.id,
            name: user.name
          })
          if (user.children) {
            addOption(user.children);
          }
        }
      })(users);

      return a
    },
    handleSubmitForm() {
      if (!this.formFields.name || !this.formFields.phone) {
        this.isFormValid = false;
        return false;
      }

      this.$emit('submit', this.formFields);
    }
  }
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
}

.form__title {
  margin: 0 0 15px 0;
}

.form__error-message {
  color: red;
  margin-bottom: 5px;
}
</style>
