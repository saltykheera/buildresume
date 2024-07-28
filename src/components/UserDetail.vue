<template>
  <v-card>
    <v-card-title>User Detail</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="name"
        label="Name"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="profile"
        label="Job Profile"
        variant="outlined"
      ></v-text-field>
    </v-card-text>
    <v-card-actions>
      <v-btn color="success" style="width: 100%;" variant="elevated" @click="saveUser">Save</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { useCounterStore } from "../stores/counter";
import { ref, inject } from "vue";

const name = ref("");
const profile = ref("");
const store = useCounterStore();
const nextComponent = inject("nextComponent"); // Inject the method

const saveUser = () => {
  store.ResumeData.push({
    userdetails: { name: name.value, jobProfile: profile.value },
  });
  console.log(store.ResumeData);
  // Clear input fields after saving
  name.value = "";
  profile.value = "";
  nextComponent(); // Move to the next component
};
</script>

<style scoped></style>
