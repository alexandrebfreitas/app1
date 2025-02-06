<template>
  <v-container class="pa-4">
    <v-card max-width="400" class="mx-auto">
      <v-card-title>Login</v-card-title>
      <v-card-text>
        <v-form @submit.prevent="submitLogin">
          <v-text-field
            label="Username"
            v-model="username"
            required
          ></v-text-field>
          <v-text-field
            label="Password"
            type="password"
            v-model="password"
            required
          ></v-text-field>
          <v-btn type="submit" color="primary" class="mt-4" block>Entrar</v-btn>
        </v-form>
        <v-alert
          v-if="error"
          type="error"
          class="mt-2"
          dismissible
        >
          {{ error }}
        </v-alert>
      </v-card-text>
      <v-card-actions>
        <v-btn text @click="$router.push('/register')">
          Não tem conta? Cadastre-se
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const router = useRouter()
const username = ref('')
const password = ref('')
const error = ref('')

const submitLogin = async () => {
  try {
    const response = await axios.post('http://localhost:8080/api/auth/login', {
      username: username.value,
      password: password.value
    })
    console.log('Usuário logado:', response.data)
    // Aqui você pode salvar o usuário no estado global ou no localStorage
    // e redirecionar para uma rota protegida (ex: /dashboard)
  } catch (err) {
    error.value = err.response.data || 'Erro no login'
  }
}
</script>
