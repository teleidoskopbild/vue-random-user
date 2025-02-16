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
  <div
    v-if="user"
    class="flex justify-center items-center h-screen bg-blue-200"
  >
    <div class="bg-blue-300 p-8 rounded-lg shadow-lg text-center w-96 h-96">
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
        <p v-if="currentInfo === 'nationality'">Nationality: {{ user.nat }}</p>
        <p v-if="currentInfo === 'dob'">Age: {{ user.dob.age }}</p>
        <p v-if="currentInfo === 'phone'">Phone: {{ user.phone }}</p>
        <p v-if="currentInfo === 'location'">
          Location: {{ user.location.city }}, {{ user.location.country }}
        </p>
      </div>

      <div class="my-4">
        <span
          @mouseover="changeInfo('email')"
          class="cursor-pointer text-xl mx-2 inline-flex justify-center items-center"
        >
          <img
            src="./assets/icons/email.svg"
            alt="Email"
            class="w-6 h-6 object-contain"
          />
        </span>

        <span
          @mouseover="changeInfo('nationality')"
          class="cursor-pointer text-xl mx-2 inline-flex justify-center items-center"
        >
          <img
            src="./assets/icons/nationality.svg"
            alt="Nationality"
            class="w-6 h-6 object-contain"
          />
        </span>

        <span
          @mouseover="changeInfo('dob')"
          class="cursor-pointer text-xl mx-2 inline-flex justify-center items-center"
        >
          <img
            src="./assets/icons/dob.svg"
            alt="Age"
            class="w-6 h-6 object-contain"
          />
        </span>

        <span
          @mouseover="changeInfo('phone')"
          class="cursor-pointer text-xl mx-2 inline-flex justify-center items-center"
        >
          <img
            src="./assets/icons/phone.svg"
            alt="Phone"
            class="w-6 h-6 object-contain"
          />
        </span>

        <span
          @mouseover="changeInfo('location')"
          class="cursor-pointer text-xl mx-2 inline-flex justify-center items-center"
        >
          <img
            src="./assets/icons/location.svg"
            alt="Location"
            class="w-6 h-6 object-contain"
          />
        </span>
      </div>

      <button
        @click="reloadUser"
        class="bg-blue-400 text-black p-2 rounded mb-4 mt-2 hover:text-white"
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
  transition: all 0.3s ease;
}
span:hover img {
  filter: invert(1);
  transition: transform 0.3s ease-in-out;
  transform: scale(1.5);
}

button {
  padding: 10px 20px;
  cursor: pointer;
}
</style>
