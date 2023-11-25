<template>
  <div>
    <v-table density="compact">
      <thead>
        <tr>
          <th class="text-left">Username</th>
          <th class="text-left">Password</th>
          <th class="text-left">Email</th>
          <th class="text-left">First Name</th>
          <th class="text-left">Last Name</th>
          <th class="text-left">Birth Day</th>
          <th class="text-left">Age</th>
          <th class="text-left">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.username }}</td>
          <td>{{ user.password }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.firstName }}</td>
          <td>{{ user.lastName }}</td>
          <td>{{ user.birthDay }}</td>
          <td>{{ user.age }}</td>
          <td>
            <v-dialog v-model="dialog" scrollable width="500">
              <template v-slot:activator="{ props }">
                <v-btn
                  color="blue"
                  size="small"
                  class="my-2 mr-2"
                  v-bind="props"
                  @click="openDialog(user)"
                  >Update</v-btn
                >
              </template>
              <v-card>
                <ModalUpdateUser :user="selectedUser" @close="closeDialog" />
              </v-card>
            </v-dialog>
            <v-btn color="red" size="small" class="my-2">Delete</v-btn>
          </td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>
<script setup>
import { ref } from "vue";
import ModalUpdateUser from "@/components/ModalUpdateUser.vue";

const props = defineProps(["users"]);

const emit = defineEmits(["updateData"]);

const dialog = ref(false);

const selectedUser = ref(null);

const openDialog = (user) => {
  selectedUser.value = user;
  dialog.value = true;
};

const closeDialog = () => {
  emit("updateData");
  selectedUser.value = null;
  dialog.value = false;
};
</script>
