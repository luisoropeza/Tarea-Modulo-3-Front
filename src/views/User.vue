<template>
  <div>
    <v-app-bar>
      <v-app-bar-title>Users</v-app-bar-title>
    </v-app-bar>
    <br />
    <v-dialog v-model="dialog" scrollable width="500">
      <template v-slot:activator="{ props }">
        <v-btn color="grey darken-1" v-bind="props">Add User</v-btn>
      </template>
      <v-card>
        <ModalCreateUser @close="closeDialog" />
      </v-card>
    </v-dialog>
    <br />
    <br />
    <UserComponent :users="users" />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import ModalCreateUser from "@/components/ModalCreateUser.vue";
import UserComponent from "@/components/UserComponent.vue";

const dialog = ref(false);

const users = ref([]);

const closeDialog = () => {
  fetchAllUsers();
  dialog.value = false;
};

const fetchAllUsers = async () => {
  try {
    const response = await axios.get(
      "http://localhost:8080/users?detailed=true"
    );
    users.value = response.data;
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

onMounted(fetchAllUsers);
</script>
