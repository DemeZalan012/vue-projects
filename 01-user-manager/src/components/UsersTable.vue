<script setup>
import { useUserStore } from '../../store/user.js'; 
import UserModal from './UserModal.vue';
import { ref } from 'vue';

const { users, removeUser } = useUserStore();

const firstNameRef = ref("");
const lastNameRef = ref("");
const emailRef = ref("");

const selectedUser = ref({});

function handleSelectedUser(user) {
  selectedUser.value = {...user}
}

async function handleDeleteUser(id) {

const valasz = confirm("Biztos törlöd?")

if (valasz) {
  try { 
    await removeUser(id) 
  }
  catch (error) {
    console.error("Hibás törlés!", error)
  }
}
}

</script>

<template>
<table class="table table-striped">
    <thead>
      <tr>
        <th><label id="firstName" name="firstName">First Name:</label> <input type="text" placeholder="" id="firstName" name="firstName" v-model="firstNameRef" /></th>
        <th><label id="lastName" name="lastName">Last Name:</label> <input type="text" placeholder="" id="lastName" name="lastName" v-model="lastNameRef" /></th>
        <th><label id="email" name="email">Email address:</label> <input type="text" placeholder="" id="email" name="email" v-model="emailRef" /></th>
        <th>-</th>
      </tr>
    </thead>

    <tbody v-for="user in users" :key="user.id">
        <tr v-if="user.firstName.includes(firstNameRef) && user.lastName.includes(lastNameRef) && user.emailAdress.includes(emailRef)">
          <td>{{ user.firstName }}</td>
          <td>{{ user.lastName }}</td>
          <td>{{ user.emailAdress }}</td>
          <td>
            <button type="button"
            class="btn btn-primary" 
            data-bs-toggle="modal" 
            data-bs-target="#editUserModal" @click="handleSelectedUser(user)">Edit</button>
            <button class="btn btn-danger" @click="handleDeleteUser(user.id)">Delete</button>
          </td>
        </tr>
    </tbody>

  </table>

  <UserModal v-if="selectedUser !== undefined" :user="selectedUser"/>
</template>

<style>
</style>