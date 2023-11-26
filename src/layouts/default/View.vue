<template>
  <v-main>
    <v-app-bar class="px-3" flat density="compact" color="deep-orange-darken-2">
      <v-spacer></v-spacer>
      <v-tabs centered>
        <v-tab v-for="link in links" :key="link.name" :to="link.link">
          {{ link.name }}
        </v-tab>
      </v-tabs>
      <v-spacer></v-spacer>
    </v-app-bar>
    <router-view />
  </v-main>
</template>

<script setup>
const links = [
  { link: "/", name: "Home" },
  { link: "/users", name: "Users" },
];
</script>
