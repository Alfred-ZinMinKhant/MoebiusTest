<script setup>
import axios from 'axios'
import { onMounted, reactive } from 'vue'
const state = reactive({
  users: [],
  loading: false,
  error: null,
})

const fetchUsers = async () => {
  state.loading = true
  try {
    // await new Promise((resolve) => setTimeout(resolve, 2000))
    const response = await axios.get('https://api.moebius.com/users')
    state.users = response.data
    console.log(state.user)
  } catch (error) {
    state.error = 'Failed to fetch users'
    console.error('Failed to fetch users', error)
  } finally {
    state.loading = false
  }
}

onMounted(fetchUsers)
</script>

<template>
  <div>
    <div v-if="state.loading">Loading...</div>
    <div v-if="state.error">{{ state.error }}</div>
    <ul v-if="state.users.length">
      <li v-for="user in state.users" :key="user.id">{{ user.name }}</li>
    </ul>
  </div>
</template>
