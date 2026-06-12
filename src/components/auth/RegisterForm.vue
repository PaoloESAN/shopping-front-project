<template>
  <q-form @submit="onSubmit" class="q-gutter-md">
    <q-input
      v-model="firstName"
      label="First Name"
      lazy-rules
      :rules="[(val: string) => !!val || 'First Name is required']"
    />

    <q-input
      v-model="lastName"
      label="Last Name"
      lazy-rules
      :rules="[(val: string) => !!val || 'Last Name is required']"
    />

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

    <q-input
      v-model="dateOfBirth"
      type="date"
      label="Date of Birth"
      lazy-rules
      :rules="[(val: string) => !!val || 'Date of Birth is required']"
    />

    <q-input
      v-model="country"
      label="Country"
      lazy-rules
      :rules="[(val: string) => !!val || 'Country is required']"
    />

    <q-input
      v-model="address"
      label="Address"
      lazy-rules
      :rules="[(val: string) => !!val || 'Address is required']"
    />

    <q-btn label="Register" type="submit" color="primary" :loading="loading" />
  </q-form>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useQuasar } from 'quasar';
import axios from 'axios';

const $q = useQuasar();

const firstName = ref('');
const lastName = ref('');
const email = ref('');
const password = ref('');
const dateOfBirth = ref('');
const country = ref('');
const address = ref('');
const loading = ref(false);

function onSubmit() {
  loading.value = true;
  axios
    .post('http://localhost:5170/api/user', {
      firstName: firstName.value,
      lastName: lastName.value,
      email: email.value,
      password: password.value,
      dateOfBirth: dateOfBirth.value,
      country: country.value,
      address: address.value,
      type: 'user',
    })
    .then(() => {
      $q.notify({
        type: 'positive',
        message: 'Registro exitoso',
        position: 'top',
      });
    })
    .catch(() => {
      $q.notify({
        type: 'negative',
        message: 'Error en el registro',
        position: 'top',
      });
    })
    .finally(() => {
      loading.value = false;
    });
}
</script>
