<template>
  <v-card>
    <v-card-title>Education</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="degree"
        label="Degree"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="institution"
        label="Institution"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="startDate"
        label="Start Date"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="endDate"
        label="End Date"
        variant="outlined"
      ></v-text-field>
      <v-textarea
        v-model="description"
        label="Description"
        rows="4"
        variant="outlined"
      ></v-textarea>
      <v-btn color="primary" @click="addEducation">Add Education</v-btn>
    </v-card-text>

    <v-divider v-if="educations.length > 0" class="my-4"></v-divider>

    <v-card v-for="(education, index) in educations" :key="index">
      <v-card-title>{{ education.degree }}</v-card-title>
      <v-card-subtitle>{{ education.institution }}</v-card-subtitle>
      <v-card-text>
        <p><strong>Start Date:</strong> {{ education.startDate }}</p>
        <p><strong>End Date:</strong> {{ education.endDate }}</p>
        <p><strong>Description:</strong></p>
        <p>{{ education.description }}</p>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-btn color="error" @click="removeEducation(index)">Delete</v-btn>
        <v-btn color="success" @click="saveEducation">Save</v-btn>
      </v-card-actions>
    </v-card>
  </v-card>
</template>

<script setup>
import { ref } from "vue";
import { useCounterStore } from "../stores/counter";

const store = useCounterStore();

const educations = ref([]);
const degree = ref("");
const institution = ref("");
const startDate = ref("");
const endDate = ref("");
const description = ref("");

const addEducation = () => {
  educations.value.push({
    degree: degree.value,
    institution: institution.value,
    startDate: startDate.value,
    endDate: endDate.value,
    description: description.value,
  });

  // Clear fields after adding
  degree.value = "";
  institution.value = "";
  startDate.value = "";
  endDate.value = "";
  description.value = "";
};

const removeEducation = (index) => {
  educations.value.splice(index, 1);
};

const saveEducation = () => {
  // Implement saving education data to a database or API
  store.ResumeData.push({ Education: educations.value });
  degree.value = "";
  institution.value = "";
  startDate.value = "";
  endDate.value = "";
  description.value = "";
  console.log(store.ResumeData);
};
</script>

<style scoped>
.my-4 {
  margin-top: 1rem;
  margin-bottom: 1rem;
}
</style>
