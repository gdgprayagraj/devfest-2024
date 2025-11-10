<template>
  <NuxtLayout name="default">
    <v-container fluid class="mt-5">
      <!-- Core Team Section -->
      <v-row>
        <v-col md="12">
          <h1>Core Team</h1>
          <p>
            Our mission is to equip our community members with practical skills,
            enabling them to communicate their insights and drive innovative
            solutions effectively. Whatever your challenge, these leaders on the
            front line of transformation, innovation, and exploration helped
            solve it with you.
          </p>
        </v-col>
      </v-row>
      <v-row>
        <v-col md="2" sm="3" cols="6" v-for="(item, index) in coreTeam" :key="index">
          <common-team-card :data="item" />
        </v-col>
      </v-row>

      <!-- Volunteers Section -->
      <v-row class="mt-8">
        <v-col md="12">
          <h1>Volunteers</h1>
          <p>
            Our dedicated volunteers contribute their time and skills to make our events successful.
            They assist with various activities including registration, logistics, and participant support.
          </p>
        </v-col>
      </v-row>
      <v-row>
        <v-col md="2" sm="3" cols="6" v-for="(item, index) in volunteers" :key="index">
          <common-team-card :data="item" />
        </v-col>
      </v-row>

      <!-- Point of Contact Section -->
      <v-row class="mt-8">
        <v-col md="12">
          <h1>Point of Contact</h1>
          <p>
            For any inquiries or assistance, please reach out to our designated contacts.
            We're here to help and provide information about our events and community activities.
          </p>
        </v-col>
      </v-row>
      <v-row>
        <v-col md="2" sm="3" cols="6" v-for="(item, index) in pointOfContact" :key="index">
          <common-team-card :data="item" />
        </v-col>
      </v-row>
    </v-container>
  </NuxtLayout>
</template>

<script setup>
const { teamData, mainData } = useJSONData();
definePageMeta({
  layout: false,
});

// Filter team members by type
const coreTeam = computed(() => {
  return teamData.filter(member => member.type === 'Core');
});

const volunteers = computed(() => {
  return teamData.filter(member => member.type === 'Volunteer');
});

const pointOfContact = computed(() => {
  return teamData.filter(member => member.type === 'Point of Contact');
});

useSeoMeta({
  contentType: "text/html; charset=utf-8",
  title: "Team - " + mainData.eventInfo.name + " | " + mainData.communityName,
  description: mainData.eventInfo.description.short,
  keywords: mainData.seo.keywords,
  ogLocale:'en_US',
  author: "GDG Prayagraj Team",
  creator: "GDG Prayagraj Team",
  viewport: "width=device-width, initial-scale=1.0",
  ogTitle: "Team - " + mainData.eventInfo.name + " | " + mainData.communityName,
  ogDescription: mainData.eventInfo.description.short,
  ogImage: `${mainData.seo.hostUrl}/thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  ogUrl: mainData.seo.hostUrl,
  ogType: "website",
  twitterTitle:
    "Team - " + mainData.eventInfo.name + " | " + mainData.communityName,
  twitterDescription: mainData.eventInfo.description.short,
  twitterImage: `${mainData.seo.hostUrl}thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  twitterCard: "summary_large_image",
});
</script>

<style scoped>
</style>