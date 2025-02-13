<script setup>
import { ref, onMounted } from "vue";

const user = ref(null);
const currentInfo = ref("email");

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

const changeInfo = (type) => {
  currentInfo.value = type;
};
</script>

<template>
  <div v-if="user">
    <h1>{{ user.name.first }} {{ user.name.last }}</h1>

    <img :src="user.picture.large" alt="User Image" />

    <div>
      <p v-if="currentInfo === 'email'">Email: {{ user.email }}</p>
      <p v-if="currentInfo === 'gender'">Gender: {{ user.gender }}</p>
      <p v-if="currentInfo === 'dob'">Age: {{ user.dob.age }}</p>
      <p v-if="currentInfo === 'phone'">Phone: {{ user.phone }}</p>
      <p v-if="currentInfo === 'location'">
        Location: {{ user.location.city }}, {{ user.location.country }}
      </p>
    </div>

    <div>
      <span @mouseover="changeInfo('email')">@</span>
      <span @mouseover="changeInfo('gender')">G</span>
      <span @mouseover="changeInfo('dob')">A</span>
      <span @mouseover="changeInfo('phone')">P</span>
      <span @mouseover="changeInfo('location')">L</span>
    </div>

    <button @click="reloadUser">Load New User</button>
  </div>
  <div v-else>
    <p>Loading...</p>
  </div>
</template>

<style scoped>
span {
  margin: 0 5px;
  padding: 5px 10px;
  cursor: pointer;
  font-weight: bold;
  color: black;
  background-color: white;
  transition: all 0.3s ease;
}

span:hover {
  color: white;
  background-color: rgb(180, 180, 180);
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  cursor: pointer;
}
</style>
