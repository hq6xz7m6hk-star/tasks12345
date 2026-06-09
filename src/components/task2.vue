<template>
  <div>
    <h2>Задание 2</h2>

    <button class="theme-btn" @click="$emit('toggle-dark')">
      {{ isDark ? '☀️ Дневной режим' : '🌙 Ночной режим' }}
    </button>

    <form class="form" @submit.prevent="submitForm">
      <div class="form-group">
        <label>Фамилия</label>
        <input v-model="form.lastName" placeholder="Введите фамилию" />
      </div>
      <div class="form-group">
        <label>Имя</label>
        <input v-model="form.firstName" placeholder="Введите имя" />
      </div>
      <div class="form-group">
        <label>Электронная почта</label>
        <input v-model="form.email" type="email" placeholder="Введите email" />
      </div>
      <div class="form-group">
        <label>Телефон</label>
        <input v-model="form.phone" type="tel" placeholder="Введите телефон" />
      </div>
      <div v-if="formError" class="error">{{ formError }}</div>
      <button type="submit">Отправить</button>
    </form>

    <div v-if="submitted" class="card">
      <h3>Данные пользователя</h3>
      <p><strong>Фамилия:</strong> {{ submitted.lastName }}</p>
      <p><strong>Имя:</strong> {{ submitted.firstName }}</p>
      <p><strong>Email:</strong> {{ submitted.email }}</p>
      <p><strong>Телефон:</strong> {{ submitted.phone }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Task2',
  props: {
    isDark: {
      type: Boolean,
      default: false
    }
  },
  emits: ['toggle-dark'],
  data() {
    return {
      form: {
        lastName:  '',
        firstName: '',
        email:     '',
        phone:     ''
      },
      submitted: null,
      formError: ''
    }
  },
  methods: {
    submitForm() {
      this.formError = ''
      const { lastName, firstName, email, phone } = this.form
      if (!lastName.trim() || !firstName.trim() || !email.trim() || !phone.trim()) {
        this.formError = 'Пожалуйста, заполните все поля!'
        return
      }
      this.submitted = { ...this.form }
    }
  }
}
</script>