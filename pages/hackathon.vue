<template>
  <NuxtLayout name="default">
    <v-container fluid class="mt-5">
      <v-row justify="center">
        <v-col md="8" cols="12">
          <div class="text-center">
            <h1 class="text-h2 font-weight-bold mb-4">🚀 Get ready to innovate with intelligence! 💡</h1>
            
            <!-- Hackathon Poster Image -->
            <v-img
              src="/public/img/hackathon/gen-ai-hackathon.jpg"
              alt="GEN-AI Hackathon Prayagraj Poster"
              class="my-6"
              style="border-radius: 20px; border: 1.5px solid black;"
              aspect-ratio="16/9"
              cover
            ></v-img>
            
            <div class="hackathon-card pa-8 my-8" style="background-color: #eeeeee; border-radius: 20px; border: 1.5px solid black;">
              <h2 class="text-h3 mb-6">Join the GEN-AI Hackathon Prayagraj</h2>
              
              <p class="text-h5 mb-4">
                A 7-hour power-packed challenge by TFUG Prayagraj where creativity meets the future of AI! 🌐⚙️
              </p>
              
              <p class="text-h5 mb-6">
                Build, innovate, and showcase your GenAI magic at DevFest Prayagraj '25! ✨
              </p>
              
              <v-btn
                href="https://forms.gle/qTDXfZ2BupcLHDDj8"
                target="_blank"
                rel="noopener noreferrer"
                size="x-large"
                class="mt-4"
                style="background-color: #4285F4; color: white; border-radius: 10px; padding: 15px 30px;"
              >
                Register Now
              </v-btn>
            </div>
            
            <div class="mt-10">
              <h3 class="text-h4 mb-4">Hackathon Details</h3>
              
              <v-row justify="center">
                <v-col md="4" sm="6" cols="12">
                  <v-card class="pa-4" style="border: 1px solid black; border-radius: 15px;">
                    <v-card-title class="text-h5">Duration</v-card-title>
                    <v-card-text class="text-h6">7 Hours</v-card-text>
                  </v-card>
                </v-col>
                
                <v-col md="4" sm="6" cols="12">
                  <v-card class="pa-4" style="border: 1px solid black; border-radius: 15px;">
                    <v-card-title class="text-h5">Organized By</v-card-title>
                    <v-card-text class="text-h6">TFUG Prayagraj</v-card-text>
                  </v-card>
                </v-col>
                
                <v-col md="4" sm="6" cols="12">
                  <v-card class="pa-4" style="border: 1px solid black; border-radius: 15px;">
                    <v-card-title class="text-h5">Focus</v-card-title>
                    <v-card-text class="text-h6">Generative AI</v-card-text>
                  </v-card>
                </v-col>
              </v-row>
            </div>
            
            <div class="mt-10">
              <h3 class="text-h4 mb-4">What to Expect</h3>
              
              <v-row justify="center">
                <v-col md="6" cols="12">
                  <v-card class="pa-4" style="border: 1px solid black; border-radius: 15px; height: 100%;">
                    <v-card-title class="text-h5">Innovation Challenge</v-card-title>
                    <v-card-text>
                      <p>Push the boundaries of what's possible with Generative AI technologies.</p>
                    </v-card-text>
                  </v-card>
                </v-col>
                
                <v-col md="6" cols="12">
                  <v-card class="pa-4" style="border: 1px solid black; border-radius: 15px; height: 100%;">
                    <v-card-title class="text-h5">Networking</v-card-title>
                    <v-card-text>
                      <p>Connect with fellow developers, AI enthusiasts, and industry experts.</p>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </NuxtLayout>
</template>

<script setup>
const { mainData } = useJSONData();

definePageMeta({
  layout: false,
});

useSeoMeta({
  contentType: "text/html; charset=utf-8",
  title: "GEN-AI Hackathon - " + mainData.eventInfo.name + " | " + mainData.communityName,
  description: "Join the GEN-AI Hackathon Prayagraj - a 7-hour power-packed challenge by TFUG Prayagraj where creativity meets the future of AI!",
  keywords: mainData.seo.keywords + ", hackathon, genai, tensorflow, tfug",
  ogLocale:'en_US',
  author: "GDG Prayagraj Team",
  creator: "GDG Prayagraj Team",
  viewport: "width=device-width, initial-scale=1.0",
  ogTitle: "GEN-AI Hackathon - " + mainData.eventInfo.name + " | " + mainData.communityName,
  ogDescription: "Join the GEN-AI Hackathon Prayagraj - a 7-hour power-packed challenge by TFUG Prayagraj where creativity meets the future of AI!",
  ogImage: `${mainData.seo.hostUrl}/thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  ogUrl: mainData.seo.hostUrl + "/hackathon",
  ogType: "website",
  twitterTitle: "GEN-AI Hackathon - " + mainData.eventInfo.name + " | " + mainData.communityName,
  twitterDescription: "Join the GEN-AI Hackathon Prayagraj - a 7-hour power-packed challenge by TFUG Prayagraj where creativity meets the future of AI!",
  twitterImage: `${mainData.seo.hostUrl}thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  twitterCard: "summary_large_image",
});
</script>

<style scoped>
.hackathon-card {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
</style>