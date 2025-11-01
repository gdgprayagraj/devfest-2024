<template>
  <v-container fluid>
    <v-alert type="warning" variant="tonal" class="my-4" style="font-size: 1.1em;">
			<strong>GEN-AI Hackathon:</strong> A 7-hour challenge, innovate, and showcase your GenAI magic. <a href="https://forms.gle/qTDXfZ2BupcLHDDj8" style="color: inherit; text-decoration: underline;">Register now</a> for this exciting opportunity! <br> <a href="/hackathon" style="color: inherit; text-decoration: underline;">Click here</a> to learn more
		</v-alert>
    <v-row>
      <v-col md="12">
        <v-container
          fluid
          style="
            background-color: #c3ecf6;
            border-radius: 20px;
            border: 1.5px solid black;
          "
        >
          <v-row justify-center align="center" class="pa-5">
            <v-col md="5" sm="6" cols="12">
              <h1 style="line-height: normal;">
                Keep in touch with {{ mainData.communityName }} for the latest
                announcements about DevFest 2025
              </h1>
              <p class="mb-3">
                Stake out #{{ mainData.communityName }} for the latest updates
                and news about building safe, secure, and scalable solutions with AI and Cloud.
              </p>

              <CommonSpeakerSocialButton
                :socialLinks="mainData.communityLinks"
              />
            </v-col>
            <v-col md="4" sm="1"></v-col>
            <v-col md="3" sm="5" cols="12">
              <v-img alt="logo" src="/assets/img/gdg-logo.svg"></v-img>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
const { mainData } = useJSONData();
</script>

<style>
</style>