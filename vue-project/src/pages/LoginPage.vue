<template>
  <div class="page center">
    <h2>Вход</h2>
    <form @submit.prevent="login">
      <input v-model="password" type="password" placeholder="Пароль (введите 'demo' или '1234')" />
      <button type="submit">Войти</button>
    </form>
    <p v-if="error" style="color: red; margin-top: 0.5rem;">
      {{ error }}
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const password = ref('')
const error = ref(null)
const router = useRouter()
const route = useRoute()

const login = () => {
  error.value = null
  if (password.value === 'demo' || password.value === '1234') {
    localStorage.setItem('token', 'demo')
    localStorage.setItem('authToken', 'demo')
    const redirectPath = route.query.redirect || { name: 'Dashboard' }
    router.push(redirectPath)
  } else {
    error.value = 'Неверный пароль. Попробуйте "demo" или "1234"'
  }
}
</script>

<style scoped>
.center { text-align: center; }
input { padding: 0.5rem; margin-right: 0.5rem; }
button { padding: 0.5rem 1rem; }
</style>