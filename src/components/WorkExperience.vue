<template>
  <v-card>
    <v-card-title>Work Experience</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="company"
        label="Company"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="position"
        label="Position"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="startDate"
        label="Start Year"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="endDate"
        label="End Year"
        variant="outlined"
      ></v-text-field>
      <v-textarea
        v-model="description"
        label="Description"
        rows="4"
        variant="outlined"
      ></v-textarea>
      <v-btn color="primary" @click="addWorkExperience"
        >Add Work Experience</v-btn
      >
    </v-card-text>

    <v-divider v-if="workExperiences.length > 0" class="my-4"></v-divider>

    <v-card v-for="(experience, index) in workExperiences" :key="index">
      <v-card-title>{{ experience.company }}</v-card-title>
      <v-card-subtitle>{{ experience.position }}</v-card-subtitle>
      <v-card-text>
        <p><strong>Start Date:</strong> {{ experience.startDate }}</p>
        <p><strong>End Date:</strong> {{ experience.endDate }}</p>
        <p><strong>Description:</strong></p>
        <p>{{ experience.description }}</p>
      </v-card-text>
      <v-card-actions>
        <v-btn color="error" @click="removeWorkExperience(index)">Delete</v-btn>
      </v-card-actions>
    </v-card>
    <v-spacer></v-spacer>
    <v-card-actions>
      <v-btn
        color="success"
        variant="elevated"
        style="width: 100%"
        @click="saveExp"
        >save</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { ref, inject } from "vue";

import { useCounterStore } from "../stores/counter";
const store = useCounterStore();

const workExperiences = ref([]);
const company = ref("");
const position = ref("");
const startDate = ref("");
const endDate = ref("");
const description = ref("");
const nextComponent = inject("nextComponent"); // Inject the method
const addWorkExperience = () => {
  workExperiences.value.push({
    company: company.value,
    position: position.value,
    startDate: startDate.value,
    endDate: endDate.value,
    description: description.value,
  });

  // Clear fields after adding
  company.value = "";
  position.value = "";
  startDate.value = "";
  endDate.value = "";
  description.value = "";
};

const removeWorkExperience = (index) => {
  workExperiences.value.splice(index, 1);
};

const saveExp = () => {
  store.ResumeData.push({ workExperiences: workExperiences.value });
  console.log(store.ResumeData);
  nextComponent();
};
</script>

<style scoped>
.my-4 {
  margin-top: 1rem;
  margin-bottom: 1rem;
}
</style>
