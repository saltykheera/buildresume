<template>
  <v-card>
    <v-card-title>Skills</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="newSkill"
        placeholder="Enter skill"
        variant="outlined"
        label="Skill"
        @keyup.enter="addSkill"
      />
      <v-btn color="primary" @click="addSkill"  >
        <v-icon>mdi-plus</v-icon>
        Add Skill</v-btn>
      <v-divider class="my-4"></v-divider>
      <div v-for="(skill, index) in skills" :key="index" class="skill-item">
        <v-chip>{{ skill }}</v-chip>
        <v-btn icon color="error" size="small" style="margin-left: 10px" @click="removeSkill(index)">
          <v-icon>mdi-delete</v-icon>
        </v-btn>
      </div>
      <v-btn color="success" style="width: 100%;" @click="saveSkills">Save Skills</v-btn>
    </v-card-text>
  </v-card>
</template>

<script setup>
import { ref, inject } from "vue";
import { useCounterStore } from "../stores/counter";

const store = useCounterStore();
const nextComponent = inject("nextComponent"); // Inject the method
const skills = ref([]);
const newSkill = ref("");

const addSkill = () => {
  if (newSkill.value.trim() !== "") {
    skills.value.push(newSkill.value.trim());
    newSkill.value = "";
  }
};

const removeSkill = (index) => {
  skills.value.splice(index, 1);
};

const saveSkills = () => {
  store.ResumeData.push({ skills: skills.value });
  nextComponent();
  console.log(store.ResumeData);
};
</script>

<style scoped>
.skill-item {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

.skill-item v-chip {
  flex-grow: 1;
}
</style>
