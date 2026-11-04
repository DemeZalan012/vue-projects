<script setup>
import { defineProps, ref, watch } from 'vue';
import { useUserStore } from '../../store/user';

const props = defineProps({
  user: {
    type: Object,
    required: true,
  }
});

const closeButton = ref();

const userFormData = ref({ ...props.user });
const { modifyUser } = useUserStore();


watch(() => props.user, (newUser) => {userFormData.value = {...newUser}}) 



async function handleSaveButton() {
  try {
    await modifyUser(userFormData.value);
    closeButton.value.click();
  } catch (error) {
    alert(error.message)
  }
}



</script>

<template>
  <div class="modal fade" id="editUserModal" tabindex="-1" aria-labelledby="editUserModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="editUserModal">Változtatás megerősítése</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <form>
        <div class="mb-3"></div>
        <label for="firstName">Keresztnév: </label>
        <input class="form-control" type="text" name="firstName" required id="firstName" v-model="userFormData.firstName">

        <div class="mb-3"></div>
        <label for="lastName">CsaládNév: </label>
        <input class="form-control" type="text" name="lastName" required id="lastName" v-model="userFormData.lastName">

        <div class="mb-3"></div>
        <label for="e-mail">E-mail: </label>
        <input class="form-control" type="text" name="e-mail" required id="e-mail" v-model="userFormData.emailAdress">
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal" ref="closeButton">Mégse</button>
        <button type="button" class="btn btn-primary" @click="handleSaveButton">Mentés</button>
      </div>
    </div>
  </div>
</div>
</template>

<style></style>