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
  <div v-if="user" class="flex justify-center items-center h-screen">
    <div class="bg-blue-400 p-8 rounded-lg shadow-lg text-center w-96 h-96">
      <h1 class="text-2xl font-semibold">
        {{ user.name.first }} {{ user.name.last }}
      </h1>

      <img
        :src="user.picture.large"
        alt="User Image"
        class="w-32 h-32 rounded-full mx-auto my-4"
      />

      <div>
        <p v-if="currentInfo === 'email'">Email: {{ user.email }}</p>
        <p v-if="currentInfo === 'gender'">Gender: {{ user.gender }}</p>
        <p v-if="currentInfo === 'dob'">Age: {{ user.dob.age }}</p>
        <p v-if="currentInfo === 'phone'">Phone: {{ user.phone }}</p>
        <p v-if="currentInfo === 'location'">
          Location: {{ user.location.city }}, {{ user.location.country }}
        </p>
      </div>

      <div class="my-4">
        <span
          @mouseover="changeInfo('email')"
          class="cursor-pointer text-xl mx-2"
          >@</span
        >
        <span
          @mouseover="changeInfo('gender')"
          class="cursor-pointer text-xl mx-2"
          >G</span
        >
        <span @mouseover="changeInfo('dob')" class="cursor-pointer text-xl mx-2"
          >A</span
        >
        <span
          @mouseover="changeInfo('phone')"
          class="cursor-pointer text-xl mx-2"
          >P</span
        >
        <span
          @mouseover="changeInfo('location')"
          class="cursor-pointer text-xl mx-2"
          >L</span
        >
      </div>

      <button
        @click="reloadUser"
        class="bg-blue-500 text-white p-2 rounded mt-4"
      >
        Load New User
      </button>
    </div>
  </div>
  <div v-else class="flex justify-center items-center h-screen">
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
