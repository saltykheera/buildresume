<template>
  <v-card>
    <v-card-title>Skills</v-card-title>
    <v-card-text>
      <v-text-field
        v-for="(skill, index) in skills"
        :key="index"
        v-model="skills[index]"
        placeholder="Enter skill"
        variant="outlined"
        label="Skill"
        @keyup.enter="addSkill"
      />
      <v-btn color="primary" @click="addSkill">Add Skill</v-btn>
      <v-divider class="my-4"></v-divider>
      <div v-for="(skill, index) in skills" :key="index" class="skill-item">
        <v-chip>{{ skill }}</v-chip>
        <v-btn icon color="error" @click="removeSkill(index)">
          <v-icon>mdi-delete</v-icon>
        </v-btn>
      </div>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  data() {
    return {
      skills: [],
    };
  },
  methods: {
    addSkill() {
      this.skills.push("");
    },
    removeSkill(index) {
      this.skills.splice(index, 1);
    },
  },
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
