<template>
  <v-container fluid class="ai-impact-section">
    <v-row justify="center" align="center">
      <v-col cols="12" class="text-center">
        <v-card 
          elevation="0" 
          class="ai-impact-card pa-6 pa-md-8"
          color="transparent"
        >
          <v-row justify="center" align="center">
            <v-col cols="12" md="4" class="d-flex justify-center align-center">
              <v-img
                src="/assets/img/India-AI-Impact-Summit-2026-Logo.png"
                alt="India AI Impact Summit 2026"
                max-width="350"
                contain
                class="ai-impact-logo"
              />
            </v-col>
            <v-col cols="12" md="8" class="text-center text-md-left">
              <h2 class="ai-impact-title mb-4">
                Official Pre-Summit Event of the 
                <a 
                  href="https://indiaai.gov.in/ai-impact-summit-2026" 
                  target="_blank"
                  class="ai-impact-link"
                >
                  AI Impact Summit 2026
                </a>
              </h2>
              <p class="ai-impact-description">
                As part of the continued efforts to collaborate with the larger ecosystem, 
                we now have the collaboration to widen the reach and prominence of DevFests in India.
              </p>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
</script>

<style scoped>
.ai-impact-section {
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  padding: 40px 0;
  margin: 40px 0;
  border-radius: 12px;
}

.ai-impact-card {
  background: rgba(255, 255, 255, 0.9);
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.18);
}

.ai-impact-logo {
  transition: transform 0.3s ease;
}

.ai-impact-logo:hover {
  transform: scale(1.05);
}

.ai-impact-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: #1e1e1e;
  line-height: 1.4;
}

.ai-impact-link {
  color: #4285f4;
  text-decoration: none;
  border-bottom: 2px solid transparent;
  transition: border-bottom 0.3s ease;
}

.ai-impact-link:hover {
  border-bottom: 2px solid #4285f4;
}

.ai-impact-description {
  font-size: 1.1rem;
  color: #5f6368;
  line-height: 1.6;
  max-width: 600px;
  margin: 0 auto;
}

@media (max-width: 960px) {
  .ai-impact-title {
    font-size: 1.4rem;
  }
  
  .ai-impact-description {
    font-size: 1rem;
  }
  
  .ai-impact-section {
    padding: 20px 0;
    margin: 20px 0;
  }
}
</style>
