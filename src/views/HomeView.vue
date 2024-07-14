<template>
  <v-main class="home-background">
    <v-container class="home-container">
      <v-row justify="center">
        <v-col cols="12" md="8" class="text-center">
          <h1 class="home-title">Build your resume here</h1>
          <v-btn @click="navigateToBuildResume" color="primary" class="mt-4">
            Build Resume
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script setup>
import { useRouter } from "vue-router";

const router = useRouter();

const navigateToBuildResume = () => {
  router.push("/buildresume");
};
</script>

<style scoped>
.home-background {
  background-color: #f0f0f0; /* Light grey background */
  height: 100vh; /* Full viewport height */
  display: flex;
  align-items: center;
}

.home-container {
  text-align: center;
}

.home-title {
  font-size: 2.5rem;
  font-weight: bold;
  color: #333; /* Dark grey text color */
}
</style>
