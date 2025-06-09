<script setup lang="ts">
import { ref, onMounted } from 'vue'
import api from '@/api/axios'

const loading = ref(true)
const apiResponse = ref(null)
const error = ref(null)

onMounted(async () => {
  try {
    const response = await api.get('/test')
    apiResponse.value = response.data
  } catch (err: any) {
    error.value = err.message || 'API Error'
  } finally {
    loading.value = false
  }
})
</script>

<template>
  <main>
    <div v-if="loading">Testing API connection...</div>
    <div v-else-if="apiResponse">API Response: {{ apiResponse }}</div>
    <div v-else-if="error">Error: {{ error }}</div>
  </main>
</template>
