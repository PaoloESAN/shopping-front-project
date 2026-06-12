<template>
  <q-form @submit="onSubmit" class="q-gutter-md">
    <q-input
      v-model="email"
      type="email"
      label="Email"
      lazy-rules
      :rules="[
        (val: string) => !!val || 'Email is required',
        (val: string) => /.+@.+/.test(val) || 'Invalid email',
      ]"
    />

    <q-input
      v-model="password"
      type="password"
      label="Password"
      lazy-rules
      :rules="[
        (val: string) => !!val || 'Password is required',
        (val: string) => val.length >= 8 || 'Min 8 characters',
      ]"
    />

    <q-btn label="Log In" type="submit" color="primary" :loading="loading" />
  </q-form>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()

const email = ref('')
const password = ref('')
const loading = ref(false)

async function onSubmit() {
  loading.value = true
  try {
    const response = await fetch('http://localhost:5170/api/user/SignIn', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email: email.value, password: password.value }),
    })

    if (response.status === 401) {
      $q.notify({
        type: 'negative',
        message: 'Credenciales inválidas',
        position: 'top',
      })
      return
    }

    if (!response.ok) {
      throw new Error('Request failed')
    }

    $q.notify({
      type: 'positive',
      message: 'Inicio de sesión exitoso',
      position: 'top',
    })
  } catch {
    $q.notify({
      type: 'negative',
      message: 'Error al iniciar sesión',
      position: 'top',
    })
  } finally {
    loading.value = false
  }
}
</script>
