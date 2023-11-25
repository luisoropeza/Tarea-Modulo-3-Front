<template>
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
</template>

<script setup>
import axios from "axios";

const emit = defineEmits(["close"]);

const props = defineProps(["user"]);

const closeDialog = () => {
  emit("close");
};

const saveAndClose = async () => {
  try {
    await axios.delete(`http://localhost:8080/users/${props.user.id}`);
    emit("close");
  } catch (error) {
    console.error("Error al eliminar el usuario:", error);
  }
};
</script>
