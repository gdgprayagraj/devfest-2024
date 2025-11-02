<template>
  <NuxtLayout name="default">
    <v-container fluid class="mt-5">
      <v-row>
        <v-col cols="12" class="text-center">
            <!-- DevFest Logo -->
            <v-img
            alt="DevFest Logo"
            src="/assets/img/devfest-logo.svg"
            lazy-src="/assets/img/devfest-logo.svg"
            max-width="200"
            class="mx-auto mb-8"
            ></v-img>
            <v-chip class="mt-n12" variant="outlined" color="black" style="background-color: white;">{{ mainData.communityLocation.city }}</v-chip>
        </v-col>
        
        <v-col cols="12">
          <h1 class="google-font">GDG Prayagraj DevFest 'Tech Trailblazer' Treasure Hunt: Code of Conduct</h1>
          <p class="mt-4">
            This Code of Conduct ensures a safe, fair, and fun environment across all participating college campuses. 
            By participating, all students agree to abide by these rules.
          </p>

          <!-- Respect and Safety Section -->
          <v-container fluid class="ma-0 pa-0 mt-8">
            <v-row>
              <v-col cols="12">
                <h2 class="google-font">1. Respect and Safety (Top Priority)</h2>
                
                <div class="mt-4">
                  <h3 class="google-font">Zero Vandalism</h3>
                  <p class="mt-2">
                    Do not damage, alter, or deface any college property while searching for QR Codes. 
                    Do not move furniture or equipment.
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">Safety First</h3>
                  <p class="mt-2">
                    Do not climb on objects, enter restricted areas (labs, staff rooms, locked rooms), 
                    or engage in any activity that risks your safety or the safety of others. 
                    Stay in public, open areas.
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">Respect Authority</h3>
                  <p class="mt-2">
                    Follow all instructions from college staff, GDG Prayagraj Admins, 
                    and the designated Points of Contact (POCs).
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">Timing</h3>
                  <p class="mt-2">
                    The hunt officially begins at 5:00 PM and must be strictly adhered to. 
                    Searching before the start time is a violation.
                  </p>
                </div>
              </v-col>
            </v-row>
          </v-container>

          <!-- Fair Play and Integrity Section -->
          <v-container fluid class="ma-0 pa-0 mt-8">
            <v-row>
              <v-col cols="12">
                <h2 class="google-font">2. Fair Play and Integrity</h2>
                
                <div class="mt-4">
                  <h3 class="google-font">Individual Participation</h3>
                  <p class="mt-2">
                    The Treasure Hunt is designed for individual students only. Group searching, 
                    collaborating on the Google Form answers, or sharing QR code locations is 
                    strictly prohibited and will result in immediate disqualification for all involved.
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">One Attempt Only</h3>
                  <p class="mt-2">
                    Once you submit the Google Form answer, that is your final attempt. 
                    Multiple form submissions will be automatically disqualified.
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">No Tampering</h3>
                  <p class="mt-2">
                    Do not remove, relocate, or cover the QR codes placed by the admins.
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">Admin Decision is Final</h3>
                  <p class="mt-2">
                    All decisions regarding winners, disqualifications, and rule interpretation 
                    rest solely with the GDG Prayagraj Core Team.
                  </p>
                </div>
              </v-col>
            </v-row>
          </v-container>

          <!-- The Process Section -->
          <v-container fluid class="ma-0 pa-0 mt-8">
            <v-row>
              <v-col cols="12">
                <h2 class="google-font">3. The Process</h2>
                
                <div class="mt-4">
                  <h3 class="google-font">Clue & Location</h3>
                  <p class="mt-2">
                    Find the QR code hidden in a public, accessible area on your campus.
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">The Challenge</h3>
                  <p class="mt-2">
                    Scan the code to access the Google Form containing a technical problem 
                    related to the DevFest 2025 theme (AI/Cloud/Security).
                  </p>
                </div>
                
                <div class="mt-4">
                  <h3 class="google-font">Submission</h3>
                  <p class="mt-2">
                    Solve the problem and submit the solution via the Google Form. 
                    The first correct submissions win.
                  </p>
                </div>
              </v-col>
            </v-row>
          </v-container>

          <!-- Prizes and Recognition Section -->
          <v-container fluid class="ma-0 pa-0 mt-8 mb-8">
            <v-row>
              <v-col cols="12">
                <h2 class="google-font">4. Prizes and Recognition</h2>
                <p class="mt-4">
                  Winners will be contacted via the email provided in the Google Form.
                </p>
                <p class="mt-2">
                  Prizes (discount codes and stickers) will be announced publicly by GDG Prayagraj.
                </p>
                <p class="mt-2">
                  Violation of this Code of Conduct will result in immediate disqualification 
                  from the Treasure Hunt and may affect eligibility for future GDG Prayagraj events.
                </p>
              </v-col>
            </v-row>
          </v-container>
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
  title: "Tech Trailblazer Treasure Hunt Code of Conduct - " + mainData.eventInfo.name + " | " + mainData.communityName,
  description: "Code of Conduct for the GDG Prayagraj DevFest Tech Trailblazer Treasure Hunt event",
  keywords: mainData.seo.keywords,
  ogLocale: 'en_US',
  author: "GDG Prayagraj Team",
  creator: "GDG Prayagraj Team",
  viewport: "width=device-width, initial-scale=1.0",
  ogTitle: "Tech Trailblazer Treasure Hunt Code of Conduct - " + mainData.eventInfo.name + " | " + mainData.communityName,
  ogDescription: "Code of Conduct for the GDG Prayagraj DevFest Tech Trailblazer Treasure Hunt event",
  ogImage: `${mainData.seo.hostUrl}/thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  ogUrl: mainData.seo.hostUrl + "/treasure-hunt-coc",
  ogType: "website",
  twitterTitle: "Tech Trailblazer Treasure Hunt Code of Conduct - " + mainData.eventInfo.name + " | " + mainData.communityName,
  twitterDescription: "Code of Conduct for the GDG Prayagraj DevFest Tech Trailblazer Treasure Hunt event",
  twitterImage: `${mainData.seo.hostUrl}thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  twitterCard: "summary_large_image",
});
</script>

<style scoped>
h1 {
  font-size: 2rem;
  font-weight: bold;
}

h2 {
  font-size: 1.5rem;
  font-weight: bold;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
  margin-bottom: 20px;
}

h3 {
  font-size: 1.2rem;
  font-weight: bold;
}
</style>