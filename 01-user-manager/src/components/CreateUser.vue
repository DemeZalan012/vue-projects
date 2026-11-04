<script setup>
import { ref } from 'vue';
const formIsVisible = ref(false);

function showForm() {
    formIsVisible.value = !formIsVisible.value;
}

</script>

<template>
    <button @click="showForm">Create new User</button>
    <form action="" v-show="formIsVisible">
        <div class="mb-3"></div>
        <label for="firstName">Keresztnév: </label>
        <input class="form-control" type="text" name="firstName" required id="firstName">

        <div class="mb-3"></div>
        <label for="lastName">CsaládNév: </label>
        <input class="form-control" type="text" name="lastName" required id="lastName">

        <div class="mb-3"></div>
        <label for="e-mail">E-mail: </label>
        <input class="form-control" type="text" name="e-mail" required id="e-mail">
    </form>
</template>