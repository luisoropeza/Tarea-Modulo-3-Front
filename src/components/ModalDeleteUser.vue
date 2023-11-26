<template>
  <v-dialog
    transition="dialog-bottom-transition"
    v-model="dialog"
    scrollable
    width="500"
  >
    <template v-slot:activator="{ props }">
      <v-btn color="red" size="small" class="my-2 mr-2" v-bind="props">
        <span><v-icon icon="mdi-pencil" style="font-size: 20px" /></span
        >Delete</v-btn
      >
    </template>
    <v-card>
      <v-card-title>
        <span class="text-h5">Delete User</span>
      </v-card-title>
      <v-card-text>
        Are you sure want to delete the user?:
        {{ user ? user.username : "User Deleted" }}
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn color="red" @click="closeDialog"> Close </v-btn>
        <v-btn color="blue" @click="saveAndClose"> Confirm </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";

const dialog = ref(false);

const props = defineProps(["user", "emit"]);

const closeDialog = () => {
  props.emit("updateData");
  dialog.value = false;
};

const saveAndClose = async () => {
  try {
    await axios.delete(`http://localhost:8080/users/${props.user.id}`);
    closeDialog();
  } catch (error) {
    console.error("Error al eliminar el usuario:", error);
  }
};
</script>
