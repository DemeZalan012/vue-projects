<script setup>
import { ref } from 'vue';
const formIsVisible = ref(false);

function showForm() {
    formIsVisible.value = !formIsVisible.value;
}

function handleSaveClick() {
    formIsVisible.value = false;
}

function handleSaveClick() {
    formIsVisible.value = false;
}

</script>

<template>
    <button @click="showForm">Create new User</button>
    <form action="" v-show="formIsVisible">
        <div class="mb-3">
        <label for="firstName">Keresztnév: </label>
        <input class="form-control" type="text" name="firstName" required id="firstName">
        </div>

        <div class="mb-3">
        <label for="lastName">CsaládNév: </label>
        <input class="form-control" type="text" name="lastName" required id="lastName">
        </div>

        <div class="mb-3">
        <label for="e-mail">E-mail: </label>
        <input class="form-control" type="email" name="e-mail" required id="e-mail">
        </div>
        
        <div class="mb-3">
            <button class="btn btn-primary" @click="handleSaveClick">Save</button>
            <button class="btn btn-secondary" @click="handleCancelClick">Cancel</button>
        </div>
    </form>
</template>