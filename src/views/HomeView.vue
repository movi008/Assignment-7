<script setup>
import { ref, computed, watch } from 'vue';

const user = ref({
  name: "John Doe",
  profileImage: "src/assets/profile.jpg",
  birthdate: "1990-01-01",
  email: "john@example.com",
  description: "Lorem ipsum dolor sit amet",
});

const birthYear = computed(() => {
  const birthYearValue = new Date(user.value.birthdate).getFullYear();
  return isNaN(birthYearValue) ? "Invalid Date" : birthYearValue;
});

const votingMessage = computed(() => {
  const age = new Date().getFullYear() - new Date(user.value.birthdate).getFullYear();
  return age >= 18 ? "Eligible for voting" : "Not eligible for voting";
});

const uploadImage = (event) => {
  const file = event.target.files[0];
  if (file) {
    user.value.profileImage = URL.createObjectURL(file);
  }
};

watch(user, (newUser, oldUser) => {
  if (newUser.birthdate !== oldUser.birthdate) {
    const age = new Date().getFullYear() - new Date(newUser.birthdate).getFullYear();
    votingMessage.value = age >= 18 ? "Eligible for voting" : "Not eligible for voting";
  }
});
</script>


<template>
  <div class="p-6">
    <div class="flex items-center">
      <div class="mr-4">
        <img :src="user.profileImage" alt="Profile Image" class="w-16 h-16 rounded-full" />
        <input type="file" @change="uploadImage" />
      </div>
      <div>
        <h1 class="text-2xl font-bold">{{ user.name }}</h1>
        <p class="text-gray-600">{{ user.email }}</p>
        <p class="text-gray-700">{{ user.description }}</p>
        <p class="mt-4">Birth Year: {{ birthYear }}</p>
        <h5 class="text-sm mt-2">{{ votingMessage }}</h5>
      </div>
    </div>
    <div class="mt-6">
      <label class="block font-bold">Name</label>
      <input v-model="user.name" class="input border border-gray-300" />

      <label class="block font-bold">Email</label>
      <input v-model="user.email" class="input border border-gray-300" />

      <label class="block font-bold mt-4">Birthdate</label>
      <input v-model="user.birthdate" class="input border border-gray-300" />
    </div>
  </div>
</template>


<style></style>