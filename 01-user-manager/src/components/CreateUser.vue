<script setup>
import { reactive, ref } from 'vue';
import { useUserStore } from '../../store/user';

const formIsVisible = ref(false);
const { addUser } = useUserStore();

const createUserForm = ref();

const userFormDataInitialState = {
    firstName: "",
    lastName: "",
    emailAdress: ""
}
const userFormData = reactive({...userFormDataInitialState})

function showForm() {
    formIsVisible.value = !formIsVisible.value;

}

async function handleSaveClick() {
    try {
    if (createUserForm.value.checkValidity()) {
    await addUser(userFormData);
    Object.assign(userFormData, userFormDataInitialState)
    }
    } catch(error) {
        alert(error.message)
    } 

}

function handleCancelClick() {
    formIsVisible.value = false;
}

</script>

<template>
    <button @click="showForm">Create new User</button>
    <form ref="createUserForm" action="" v-show="formIsVisible" >
        <div class="mb-3">
        <label for="firstName">Keresztnév: </label>
        <input class="form-control" type="text" name="firstName" required id="firstName" v-model="userFormData.firstName">
        </div>

        <div class="mb-3">
        <label for="lastName">CsaládNév: </label>
        <input class="form-control" type="text" name="lastName" required id="lastName" v-model="userFormData.lastName">
        </div>

        <div class="mb-3">
        <label for="e-mail">E-mail: </label>
        <input class="form-control" type="email" name="e-mail" required id="e-mail" v-model="userFormData.emailAdress">
        </div>
        
        <div class="mb-3">
            <button type="button" class="btn btn-primary" @click.prevent="handleSaveClick">Save</button>
            <button class="btn btn-secondary" @click="handleCancelClick">Cancel</button>
        </div>
    </form>
</template>