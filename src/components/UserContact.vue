<template>
  <v-card>
    <v-card-title>User Contact</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="email"
        label="Email"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="phone"
        label="Phone"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="location"
        label="Location"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="twitter"
        label="Twitter"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="linkedin"
        label="LinkedIn"
        variant="outlined"
      ></v-text-field>
    </v-card-text>
    <v-card-actions>
      <v-btn color="success" variant="elevated" @click="saveContact"
        >Save</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { useCounterStore } from "../stores/counter";
import { ref } from "vue";

const email = ref("");
const phone = ref("");
const location = ref("");
const twitter = ref("");
const linkedin = ref("");
const store = useCounterStore();

const saveContact = () => {
  store.ResumeData.push({
    userContact: {
      email: email.value,
      phone: phone.value,
      location: location.value,
      twitter: twitter.value,
      linkedin: linkedin.value,
    },
  });

  // Clear input fields after saving
  email.value = "";
  phone.value = "";
  location.value = "";
  twitter.value = "";
  linkedin.value = "";
  console.log(store.ResumeData)
};
</script>

<style scoped></style>
