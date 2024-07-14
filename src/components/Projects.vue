<template>
  <v-card>
    <v-card-title>Projects</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="title"
        label="Project Title"
        variant="outlined"
      ></v-text-field>
      <v-text-field
        v-model="link"
        label="Project Link"
        variant="outlined"
      ></v-text-field>
      <v-textarea
        v-model="description"
        label="Description"
        rows="4"
        variant="outlined"
      ></v-textarea>
      <v-btn color="primary" @click="addProject">Add Project</v-btn>
    </v-card-text>

    <v-divider v-if="projects.length > 0" class="my-4"></v-divider>

    <v-card v-for="(project, index) in projects" :key="index">
      <v-card-title>{{ project.title }}</v-card-title>
      <v-card-subtitle v-if="project.link">{{ project.link }}</v-card-subtitle>
      <v-card-text>{{ project.description }}</v-card-text>
      <v-card-actions>
        <v-btn color="error" @click="removeProject(index)">Delete</v-btn>
      </v-card-actions>
    </v-card>
    <v-card-actions>
      <v-btn color="success" variant="elevated" @click="saveProjects"
        >save</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { ref,inject } from "vue";
import { useCounterStore } from "../stores/counter";

const store = useCounterStore();

const projects = ref([]);
const title = ref("");
const link = ref("");
const description = ref("");
const nextComponent = inject("nextComponent"); // Inject the method
const addProject = () => {
  projects.value.push({
    title: title.value,
    link: link.value,
    description: description.value,
  });

  // Clear fields after adding
  title.value = "";
  link.value = "";
  description.value = "";
};

const removeProject = (index) => {
  projects.value.splice(index, 1);
};
const saveProjects = () => {
  store.ResumeData.push({ Projects: projects.value });
  nextComponent();
};
</script>

<style scoped>
.my-4 {
  margin-top: 1rem;
  margin-bottom: 1rem;
}
</style>
