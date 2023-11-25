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
            <v-btn color="red" size="small" class="my-2 mr-2">Eliminar</v-btn>
            <v-btn color="blue" size="small" class="my-2">Editar</v-btn>
          </td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>
<script setup>
const props = defineProps(["users"]);
</script>
