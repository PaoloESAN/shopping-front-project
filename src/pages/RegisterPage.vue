<template>
  <q-page class="flex flex-center">
    <q-card style="width: 450px; max-width: 90vw">
      <q-card-section>
        <div class="text-h5 text-center q-mb-md">Register</div>
        <RegisterForm />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup lang="ts">
import RegisterForm from '@/components/auth/RegisterForm.vue'
</script>
