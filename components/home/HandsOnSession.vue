<template>
  <v-container fluid>
    <v-row>
      <v-col cols="12">
        <div
          style="background-color: #eeeeee; border-radius: 15px; border: 1.5px solid black;"
          class="pa-6"
        >
          <h1>Hands-on Sessions</h1>
          <p>
            Get practical experience with our interactive hands-on sessions led by industry experts.
          </p>
          
          <!-- <v-container fluid>
            <v-row justify-start align="start">
              <v-col
                v-for="(session, index) in handsOnSessions"
                :key="index"
                md="4"
                sm="6"
                cols="12"
              >
                <v-card
                  style="border: 1px solid black; border-radius: 10px;"
                  class="pa-4 h-100"
                >
                  <v-card-title class="text-h6">{{ session.title }}</v-card-title>
                  <v-card-text>
                    <p class="text-body-2">{{ session.description }}</p>
                    <div class="d-flex align-center mt-2">
                      <v-icon small class="mr-2">mdi-clock-outline</v-icon>
                      <span class="text-caption">{{ session.time }}</span>
                    </div>
                    <div class="d-flex align-center mt-1" v-if="session.track">
                      <v-icon small class="mr-2">mdi-tag-outline</v-icon>
                      <span class="text-caption">{{ session.track }}</span>
                    </div>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-container> -->
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
const { mainData } = useJSONData();

// Define hands-on sessions data
const handsOnSessions = ref([
  {
    title: "Generative AI for Future Trends",
    description: "Dive deep into AI and Generative AI and its potential impact on web development, highlighting real-world use cases and future trends.",
    time: "10:30 AM to 11:00 AM (IST)",
    track: "AI"
  },
  {
    title: "Utilize the Power of AI with Flutter App Development",
    description: "Explore the integration of AI into Flutter applications, demonstrating how developers can make their mobile apps smarter.",
    time: "1:30 PM to 2:00 PM (IST)",
    track: "Flutter"
  },
  {
    title: "Serverless AI with Cloud Run GPU",
    description: "Learn how to deploy AI models in a serverless environment using Google Cloud Run with GPU.",
    time: "11:30 AM to 12:00 PM (IST)",
    track: "Cloud & ML"
  }
]);
</script>

<style scoped>
</style>