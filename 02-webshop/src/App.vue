<script setup>
import { onMounted } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import { useGuitarStore } from './store/guitars.js'

const { guitars, fetchGuitars } = useGuitarStore()

onMounted(async () => {
  await fetchGuitars()
  console.log(guitars.value)
})
</script>

<template>
<p></p>
</template>

<style scoped>

</style>
