<template>
  <div class="entry-content">
    <div class="login">
      <h1>Регистрация</h1>
      <form @submit.prevent="login">
        <!-- Добавлено @submit.prevent для вызова метода login -->
        <p>
          <input type="text" v-model="username" placeholder="Логин" />
          <!-- Связка с username -->
        </p>
        <p>
          <input type="password" v-model="password" placeholder="Пароль" />
          <!-- Связка с password -->
        </p>
        <p class="remember_me">
          <label><input type="checkbox" name="remember_me" />Запомнить меня</label>
        </p>
        <p class="submit">
          <input type="submit" value="Зарегистрироваться" />
        </p>
      </form>
    </div>
    <div class="clearfix"></div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "API2Vue",
  data() {
    return {
      username: "",
      surname: "",
    };
  },
  methods: {
    login() {
      // Убрано event, обработчик вызван через @submit.prevent
      // логика регистрации
      axios
        .post("http://localhost:8000/api/user", {
          name: this.username, // Исправлено: используем this.username
          surname: this.password,
        })
        .then((response) => {
          this.setLogined(response.data.token);
        })
        .catch((err) => {
          console.error(err); // Логирует ошибку в консоль
        });
    },

    setLogined(token) {
      console.log(token); // Выводит токен в консоль
    },
  },
};
</script>
