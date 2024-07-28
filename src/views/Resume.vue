<template>
  <v-main
    class="resume-builder"
    style="background-color: #d8e9f7; min-height: 100vh"
  >
    <v-container class="build-section" v-if="!endPage">
      <v-row justify="center">
        <v-col cols="12" md="8">
          <component :is="components[currentComponent]" />
        </v-col>
      </v-row>
      <!-- <v-row justify="space-between" class="navigation-buttons">
        <v-col cols="12" sm="6">
          <v-btn
            variant="elevated"
            class="font-weight-bold"
            color="grey"
            @click="previousComponent"
            :disabled="currentComponent === 0"
            style="width: 100%; font-size: 1.1rem"
          >
            Back
          </v-btn>
        </v-col>
        <v-col cols="12" sm="6">
          <v-btn
            variant="elevated"
            class="font-weight-bold"
            color="primary"
            @click="nextComponent"
            style="width: 100%; font-size: 1.1rem"
          >
            Next
          </v-btn>
        </v-col>
      </v-row> -->
    </v-container>

    <v-container class="end" v-if="endPage">
      <v-row justify="center">
        <v-col cols="12" class="text-center">
          <h2>You've reached the end!</h2>
        </v-col>
      </v-row>
      <v-row justify="center">
        <v-col cols="12" sm="6">
          <v-btn
            @click="buildResume"
            variant="elevated"
            color="success"
            style="width: 100%; font-size: 1.1rem"
          >
            <v-icon class="mr-2">mdi-wrench</v-icon>
            Build Resume
          </v-btn>
        </v-col>
        <v-col cols="12" sm="6">
          <v-btn
            variant="elevated"
            class="font-weight-bold"
            color="primary"
            @click="previousComponent"
            style="width: 100%; font-size: 1.1rem"
          >
            <v-icon class="mr-2">mdi-arrow-left</v-icon>
            Back
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script setup>
import { ref, provide } from "vue";
import { useRouter } from "vue-router";
import UserDetail from "../components/UserDetail.vue";
import UserContact from "../components/UserContact.vue";
import Skill from "../components/Skill.vue";
import Education from "../components/Education.vue";
import Achievement from "../components/Achievement.vue";
import WorkExperience from "../components/WorkExperience.vue";
import Projects from "../components/Projects.vue";
import { useCounterStore } from "../stores/counter";

const store = useCounterStore();
const router = useRouter();
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

const buildResume = () => {
  alert("Resume Created!");
  const proxyobj = store.ResumeData;
  const jsonstr = JSON.stringify(proxyobj);
  console.log("this is jsonstr");
  router.push("/about");
  console.log(jsonstr);
  const cleanObject = JSON.parse(jsonstr);
  console.log("this is the final object");
  console.log(cleanObject);
};

provide("nextComponent", nextComponent); // Provide the method
</script>

<style scoped>
.resume-builder {
  height: 100vh; /* Full viewport height */
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.build-section,
.end {
  text-align: center;
  max-width: 800px; /* Adjust maximum width as needed */
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.build-section {
  transform: translateY(0);
}

.end {
  transform: translateY(-50px);
}

.navigation-buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
}
</style>
