<template>
  <div>
    <form @submit.prevent="submitForm">
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="formData.username" required>

      <label for="password">Password:</label>
      <input type="password" id="password" v-model="formData.password" required>

      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        username: '',
        password: '',
      },
    };
  },
  methods: {
    async submitForm() {
      try {
        // Используйте Axios для отправки данных на ваш сервер
        const response = await this.$axios.post('/auth/save-user', this.formData);

        if (response && response.data) {
          console.log(response.data); // Реакция на успешный ответ
        } else {
          console.error('Error: Empty response or response.data is undefined');
        }
      } catch (error) {
        console.error('Error:', error.response ? error.response.data : error.message); // Реакция на ошибку
      }
    },
  },
};
</script>
