<template>
  <v-app>
    <v-app-bar color="primary" dark app>
      <v-app-bar-title>Build Resume</v-app-bar-title>
      <v-spacer></v-spacer>
      <v-btn text>Login</v-btn>
      <v-btn outlined>Sign Up</v-btn>
    </v-app-bar>

    <v-main>
      <!-- Hero Section -->
      <v-container fluid class="pa-0">
        <v-row no-gutters>
          <v-col cols="12">
            <v-sheet
              class="d-flex flex-column align-center justify-center text-center pa-16"
              color="grey-lighten-4"
              height="100vh"
            >
              <h1 class="text-h2 font-weight-bold mb-4">
                Build Your Resume
              </h1>
              <h2 class="text-h4 font-weight-regular mb-8">
                Simple, Easy, and Free
              </h2>
              <v-btn
                x-large
                color="primary"
                size="x-large"
                class="text-capitalize"
                @click="startBuilding"
              >
                Start Building for Free
              </v-btn>
            </v-sheet>
          </v-col>
        </v-row>
      </v-container>

      <!-- Features Section -->
      <v-container class="py-16">
        <v-row>
          <v-col cols="12" class="text-center mb-12">
            <h2 class="text-h3 font-weight-bold">Why Choose Build Resume?</h2>
          </v-col>
        </v-row>
        <v-row>
          <v-col v-for="feature in features" :key="feature.title" cols="12" md="4">
            <v-card class="mx-auto" max-width="400" height="100%">
              <v-card-item>
                <v-icon
                  :icon="feature.icon"
                  size="64"
                  class="mb-4"
                  color="primary"
                ></v-icon>
                <v-card-title class="text-h5 mb-2">{{ feature.title }}</v-card-title>
                <v-card-text>{{ feature.description }}</v-card-text>
              </v-card-item>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <v-footer app color="primary" dark class="py-4">
      <v-container>
        <v-row no-gutters align="center" justify="center">
          <v-col cols="12" class="text-center">
            &copy; {{ new Date().getFullYear() }} Build Resume. All rights reserved.
          </v-col>
        </v-row>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const features = ref([
  {
    icon: 'mdi-flash',
    title: 'Quick and Easy',
    description: 'Create a professional resume in minutes with our intuitive builder.'
  },
  {
    icon: 'mdi-currency-usd-off',
    title: '100% Free',
    description: 'No hidden fees or premium features. All tools are completely free.'
  },
  {
    icon: 'mdi-palette',
    title: 'Customizable Templates',
    description: 'Choose from a variety of modern, ATS-friendly resume templates.'
  }
])

const startBuilding = () => {
  // Navigate to the resume builder page
  router.push('/buildresume')
}
</script>

<style scoped>
/* Add any component-specific styles here */
</style>
