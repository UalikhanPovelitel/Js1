<template>
  <div id="app">
    <h1>Авторизация</h1>
    
    <div class="button-group">
      <button @click="showRegistration" :class="{ active: isRegistering }">Регистрация</button>
      <button @click="showLogin" :class="{ active: !isRegistering }">Вход</button>
    </div>

    <form v-if="isRegistering" @submit.prevent="register">
      <div>
        <label for="name">Имя:</label>
        <input type="text" id="name" v-model="name" required>
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" required>
      </div>
      <div>
        <label for="password">Пароль:</label>
        <input type="password" id="password" v-model="password" required>
      </div>
      <button type="submit">Зарегистрироваться</button>
    </form>

    <form v-else @submit.prevent="login">
      <div>
        <label for="login-email">Email:</label>
        <input type="email" id="login-email" v-model="loginEmail" required>
      </div>
      <div>
        <label for="login-password">Пароль:</label>
        <input type="password" id="login-password" v-model="loginPassword" required>
      </div>
      <button type="submit">Войти</button>
    </form>

    <!-- Вставляем компонент списка товаров -->
    <ProductList v-if="loggedIn" />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue'

export default {
  components: {
    ProductList
  },
  data() {
    return {
      isRegistering: true, // Состояние для отображения формы регистрации или входа
      name: '',
      email: '',
      password: '',
      submitted: false,
      loginEmail: '',
      loginPassword: '',
      loginSubmitted: false,
      loggedIn: false
    };
  },
  methods: {
    showRegistration() {
      this.isRegistering = true; // Показываем форму регистрации
    },
    showLogin() {
      this.isRegistering = false; // Показываем форму входа
    },
    register() {
      this.submitted = true;
      console.log('Регистрация прошла успешно:', this.name, this.email);
    },
    login() {
      this.loginSubmitted = true;
      this.loggedIn = true; // Устанавливаем состояние пользователя
      console.log('Вход выполнен:', this.loginEmail);
    }
  }
}
</script>

<style>
.button-group {
  display: flex; /* Используем Flexbox для расположения кнопок */
  justify-content: center; /* Центруем кнопки по горизонтали */
  margin-bottom: 20px; /* Отступ снизу */
}

.button-group button {
  margin: 0 10px; /* Отступы между кнопками */
  padding: 10px 20px; /* Отступы внутри кнопок */
  border: 1px solid #ccc; /* Рамка кнопок */
  border-radius: 5px; /* Скругление углов кнопок */
  cursor: pointer; /* Курсор при наведении */
}

.button-group button.active {
  background-color: #007bff; /* Цвет фона для активной кнопки */
  color: white; /* Цвет текста для активной кнопки */
}

button[type="submit"] {
  margin-top: 10px; /* Отступ сверху для кнопки отправки */
}
</style>
