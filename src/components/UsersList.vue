<template>
  <div class="px-10">
    <div>
      <table class="w-full">
        <thead>
          <tr class="py-4">
            <th class="py-4 px-4 text-start text-sm text-[#ACACAC]">ID</th>
            <th class="py-4 px-4 text-start text-sm text-[#ACACAC]">Name</th>
            <th class="py-4 px-4 text-start text-sm text-[#ACACAC]">Email</th>
            <th class="py-4 px-4 text-start text-sm text-[#ACACAC]">Phone</th>
            <!-- <th class="py-4 px-4 text-start text-sm text-[#ACACAC]">
              Enroll Number
            </th>
            <th class="py-4 text-start text-sm text-[#ACACAC]">
              Date of admission
            </th> -->
            <th class="py-4 text-start text-sm text-[#ACACAC]">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(user, index) in users" :key="user.id" class="border">
            <td class="bg-white py-3 px-4">{{ index + 1 }}</td>
            <td class="bg-white py-3 px-4">{{ user.full_name }}</td>
            <td class="bg-white py-3 px-4">{{ user.email }}</td>
            <td class="bg-white py-3 px-4">{{ user.phone_number }}</td>
            <!-- <td class="bg-white py-3 px-4">{{ user.enrollNumber }}</td>
            <td class="bg-white py-3 px-4">{{ user.dateOfAdmission }}</td> -->
            <td class="bg-white py-3 px-4">
              <div class="flex gap-x-8">
                <span>Edit</span>
                <span>Delete</span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      <!-- <AddUserModal /> -->
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import AddUserModal from "./AddUserModal.vue";

const users = ref([]);

const fetchUsers = async () => {
  try {
    const api = await axios.get("https://tour.touristan-bs.uz/v1/users/list?limit=10&page=1&column=role&value=user", {
      headers: {
        accept: "application/json",
        Authorization:
          "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MTg5MjUyNTgsImlhdCI6MTcxODIwNTI1OCwiaXNzIjoiIiwicm9sZSI6InN1ZG8iLCJzdWIiOiIyZTljYTI3Ni01Nzk5LTRmMzQtYTBhNi05MzhmN2IwYTVjOGQifQ.vG377oKJy4IwE_tp8ob2CJXDRsRP3nAS_kMQkqRkQa0",
      },
    });
    users.value = api.data.users;
    console.log(users.value.users);
  } catch (error) {
    console.error("Error fetching users:", error);
  }
};

onMounted(fetchUsers);
</script>

<style lang="scss" scoped></style>
