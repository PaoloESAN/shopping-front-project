<template>
  <q-page class="flex flex-center">
    <q-card style="width: 400px; max-width: 90vw">
      <q-card-section>
        <div class="text-h5 text-center q-mb-md">Log In</div>
        <LogInForm />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup lang="ts">
import LogInForm from '@/components/auth/LogInForm.vue'
</script>
