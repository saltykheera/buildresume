<template>
  <div>
    <div class="build-section" v-if="!endPage" style="min-width: 600px">
      <component :is="components[currentComponent]" />
      <div class="navigation-buttons">
        <v-btn
          variant="elevated"
          class="font-weight-bold mt-2"
          color="grey"
          @click="previousComponent"
          :disabled="currentComponent === 0"
          >Back</v-btn
        >
        <v-btn
          variant="elevated"
          class="font-weight-bold mt-2"
          color="primary"
          @click="nextComponent"
          >Next</v-btn
        >
      </div>
      <p>{{ currentComponent }}</p>
    </div>

    <div class="end" v-if="endPage">
      <h2>You've reached the end!</h2>
      <v-btn @click="BuildResume" variant="elevated" color="success"
        >Build Resume</v-btn
      >
      <v-btn
        variant="elevated"
        class="font-weight-bold mt-2"
        color="primary"
        @click="previousComponent"
        >Back</v-btn
      >
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import UserDetail from "../components/UserDetail.vue";
import UserContact from "../components/UserContact.vue";
import Skill from "../components/Skill.vue";
import Education from "../components/Education.vue";
import Achievement from "../components/Achievement.vue";
import WorkExperience from "../components/WorkExperience.vue";
import Projects from "../components/Projects.vue";

import { useCounterStore } from "../stores/counter";

const store = useCounterStore();

const components = [
  UserDetail,
  UserContact,
  Skill,
  Education,
  Achievement,
  WorkExperience,
  Projects,
];

const currentComponent = ref(0);
const endPage = ref(false);

const nextComponent = () => {
  if (currentComponent.value < components.length - 1) {
    currentComponent.value++;
  } else {
    endPage.value = true;
  }
};

const previousComponent = () => {
  if (currentComponent.value > 0) {
    currentComponent.value--;
  }
  if (endPage.value) {
    endPage.value = false;
  }
};

const BuildResume = () => {
  alert("Resume Created!");
  const proxyobj = store.ResumeData;
  const jsonstr = JSON.stringify(proxyobj);
  console.log("this is jsonstr");
  console.log(jsonstr);
  const cleanObject = JSON.parse(jsonstr);
  console.log("this is the final object");
  console.log(cleanObject);
};
</script>

<style>
/* Add any necessary styles here */
.navigation-buttons {
  display: flex;
  gap: 10px;
}
</style>
