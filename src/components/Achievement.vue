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
      <v-btn color="success" @click="addAchievement">SAVE</v-btn>
      <v-divider class="my-4"></v-divider>
      <div v-for="(achievement, index) in achievements" :key="index">
        <v-card class="mb-2">
          <v-card-title>{{ achievement.title }}</v-card-title>
          <v-card-text>{{ achievement.description }}</v-card-text>
          <v-btn color="error" @click="removeAchievement(index)">DELETE</v-btn>
        </v-card>
      </div>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  data() {
    return {
      newAchievement: {
        title: "",
        description: "",
      },
      achievements: [],
    };
  },
  methods: {
    addAchievement() {
      if (this.newAchievement.title && this.newAchievement.description) {
        this.achievements.push({ ...this.newAchievement });
        this.newAchievement.title = "";
        this.newAchievement.description = "";
      }
    },
    removeAchievement(index) {
      this.achievements.splice(index, 1);
    },
  },
};
</script>
