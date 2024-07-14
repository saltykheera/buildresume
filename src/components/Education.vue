<template>
  <v-card>
    <v-card-title>Education</v-card-title>
    <v-card-text>
      <v-text-field label="Degree" variant="outlined"></v-text-field>
      <v-text-field label="Institution" variant="outlined"></v-text-field>
      <v-text-field label="Start Date" variant="outlined"></v-text-field>
      <v-text-field label="End Date" variant="outlined"></v-text-field>
      <v-textarea label="Description" rows="4" variant="outlined"></v-textarea>
    </v-card-text>
    <v-card-actions>
      <v-btn color="primary" @click="addEducation">Add Education</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  methods: {
    addEducation() {
      // Add logic for adding education
    },
  },
};
</script>

<style scoped></style>
