<script setup lang="ts">
const router = useRouter()
onMounted(() => {
  router.push('/tasks')
})
</script>

<template>
  <router-link to="/tasks">
    cool
  </router-link>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
