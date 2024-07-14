<template>
  <v-card>
    <v-card-title>Achievements</v-card-title>
    <v-card-text>
      <v-text-field
        v-model="newAchievement.title"
        label="Achievement Title"
        variant="outlined"
      ></v-text-field>
      <v-textarea
        v-model="newAchievement.description"
        label="Achievement Description"
        rows="4"
        variant="outlined"
      ></v-textarea>
      <v-btn color="primary" @click="addAchievement">Add Achievement</v-btn>
      <v-divider class="my-4"></v-divider>
      <div v-for="(achievement, index) in achievements" :key="index">
        <v-card class="mb-2">
          <v-card-title>{{ achievement.title }}</v-card-title>
          <v-card-text>{{ achievement.description }}</v-card-text>
          <v-btn color="error" @click="removeAchievement(index)">DELETE</v-btn>
        </v-card>
      </div>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="success" variant="elevated" @click="saveAchievements"
        >SAVE</v-btn
      >
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { ref } from "vue";
import { useCounterStore } from "../stores/counter";

const store = useCounterStore();

const newAchievement = ref({
  title: "",
  description: "",
});

const achievements = ref([]);

const addAchievement = () => {
  if (newAchievement.value.title && newAchievement.value.description) {
    achievements.value.push({ ...newAchievement.value });
    newAchievement.value.title = "";
    newAchievement.value.description = "";
  }
};

const removeAchievement = (index) => {
  achievements.value.splice(index, 1);
};

const saveAchievements = () => {
  // Save achievements to a database or file
  store.ResumeData.push({ achievements: achievements.value });
  console.log(store.ResumeData);
};
</script>
