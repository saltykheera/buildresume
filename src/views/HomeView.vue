<template>
  <v-main class="home-background">
    <v-container class="home-container" style="background-color: #d8e9f7">
      <v-row justify="center">
        <v-col cols="12" md="8" class="text-center">
          <h1 class="home-title" style="font-size: 64px">
            Build your Resume Here
          </h1>
          <p style="color: #626262">
            The best Free Resume Builder tool to
            <span style="color: #0086f7">visualize</span>,
            <span style="color: #0086f7">format</span>
            and
            <span style="color: #0086f7">modify</span>.
          </p>
          <v-btn
            @click="navigateToBuildResume"
            size="large"
            style="font-size: 12px; font-weight: bold"
            color="primary"
            class="mt-4"
            variant="outlined"
            rounded
          >
            Build Resume
          </v-btn>
        </v-col>
      </v-row>
      <v-row justify="center">
        <v-col cols="12" class="text-center">
          <v-divider class="my-4"></v-divider>
        </v-col>
      </v-row>
      <v-row justify="center">
        <v-col cols="12" md="8" class="text-center">
          <div
            class="guideHome d-flex align-center justify-center flex-column flex-md-row"
            style="gap: 2rem"
          >
            <v-img width="500px" src="/docDraw.svg"></v-img>
            <div class="guideList mx-2">
              <v-row justify="center" align="center" class="guideList">
                <v-col cols="12" class="text-center guideitems">
                  <v-icon large class="white--text">mdi-eye</v-icon>
                  <h3 class="white--text">Visualize your Resume</h3>
                  <p class="white--text">Create a visually appealing resume</p>
                </v-col>
                <v-col cols="12" class="text-center guideitems">
                  <v-icon large class="white--text"
                    >mdi-format-list-bulleted</v-icon
                  >
                  <h3 class="white--text">Format your Resume</h3>
                  <p class="white--text">
                    Choose your desired format and layout
                  </p>
                </v-col>
                <v-col cols="12" class="text-center guideitems">
                  <v-icon large class="white--text">mdi-pencil</v-icon>
                  <h3 class="white--text">Modify your Resume</h3>
                  <p class="white--text">
                    Make necessary changes to your resume
                  </p>
                </v-col>
              </v-row>
            </div>
          </div>
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
  background-color: #9bbdd7; /* Light grey background */
  min-height: 100vh; /* Full viewport height */
  display: flex;
  align-items: center;
  justify-content: center;
}

.home-container {
  text-align: center;
}

.home-title {
  font-size: 2.5rem;
  font-weight: bold;
  color: #333; /* Dark grey text color */
}

.white--text {
  color: #333; /* White text color */
}

.guideitems {
  margin-bottom: 1rem;
}

/* Additional styling for responsive design */
.guideHome {
  display: flex;
  flex-direction: column;
}

@media (min-width: 600px) {
  .guideHome {
    flex-direction: row;
  }
}
</style>
