<script setup>
import { ref, onMounted } from "vue";

const user = ref(null);

const fetchUser = async () => {
  const response = await fetch("https://randomuser.me/api/");
  const data = await response.json();
  user.value = data.results[0];
};

onMounted(() => {
  fetchUser();
});

const reloadUser = () => {
  fetchUser();
};
</script>

<template>
  <div v-if="user">
    <h1>{{ user.name.first }} {{ user.name.last }}</h1>
    <img :src="user.picture.large" alt="User Image" />
    <p>Email: {{ user.email }}</p>
    <p>Location: {{ user.location.city }}, {{ user.location.country }}</p>
    <button @click="reloadUser">Load new user</button>
  </div>
  <div v-else>
    <p>Loading...</p>
  </div>
</template>

<style scoped></style>
