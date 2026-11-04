<script setup>
import { useUserStore } from '../store/user';
import CreateUser from './components/CreateUser.vue';
import Users_table from './components/UsersTable.vue';

const { fetchUsers } = useUserStore();

try {
  fetchUsers();
} catch (error) {
  console.error("Felhasználók betoltése sikertelen", error)
}

</script>

<template>
  <div class="container">
    <CreateUser/>
    <Users_table/>
  </div>

</template>

<style scoped>

</style>
