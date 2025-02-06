<template>
  <v-container class="pa-4">
    <v-card max-width="400" class="mx-auto">
      <v-card-title>Cadastro</v-card-title>
      <v-card-text>
        <v-form @submit.prevent="submitRegister">
          <v-text-field
            label="Username"
            v-model="username"
            required
          ></v-text-field>
          <v-text-field
            label="Email"
            type="email"
            v-model="email"
            required
          ></v-text-field>
          <v-text-field
            label="Password"
            type="password"
            v-model="password"
            required
          ></v-text-field>
          <v-btn type="submit" color="primary" class="mt-4" block>Cadastrar</v-btn>
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
        <v-btn text @click="$router.push('/login')">
          Já possui conta? Faça login
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
const email = ref('')
const password = ref('')
const error = ref('')

const submitRegister = async () => {
  try {
    const response = await axios.post('http://localhost:8080/api/auth/register', {
      username: username.value,
      email: email.value,
      password: password.value
    })
    console.log('Usuário cadastrado:', response.data)
    router.push('/login')
  } catch (err) {
    error.value = err.response.data || 'Erro no cadastro'
  }
}
</script>
