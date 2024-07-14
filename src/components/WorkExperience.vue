<template>
  <v-card>
    <v-card-title>Work Experience</v-card-title>
    <v-card-text>
      <v-text-field label="Company" variant="outlined"></v-text-field>
      <v-text-field label="Position" variant="outlined"></v-text-field>
      <v-text-field label="Start Date" variant="outlined"></v-text-field>
      <v-text-field label="End Date" variant="outlined"></v-text-field>
      <v-textarea label="Description" rows="4" variant="outlined"></v-textarea>
    </v-card-text>
    <v-card-actions>
      <v-btn color="primary" @click="addWorkExperience"
        >Add Work Experience</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  methods: {
    addWorkExperience() {
      // Add logic for adding work experience
    },
  },
};
</script>

<style scoped></style>
