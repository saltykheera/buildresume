<template>
  <main>
    <h1>Build your resume here</h1>
    <v-btn @click="navigateToBuildResume">Build Resume</v-btn>
  </main>
</template>

<script setup>
import { useRouter } from "vue-router";

const router = useRouter();

const navigateToBuildResume = () => {
  router.push("/buildresume");
};
</script>
