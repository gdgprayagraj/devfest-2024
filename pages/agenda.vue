<template>
  <NuxtLayout name="default">
    <v-container fluid class="mt-5">
      <v-row>
        <v-col md="12">
          <h1 class="google-font agenda-page-title">Agenda</h1>
          <p class="google-font agenda-page-description mb-8">
            Follow code demonstrations by our expert speakers on different
            tracks. Check out the schedule below and don't forget to mark your
            calendar so that you don't miss out on any sessions.
          </p>
        </v-col>
      </v-row>

      <!-- Agenda Timeline -->
      <v-row class="mb-7">
        <v-col md="12">
          <v-card
            class="agenda-container google-font"
            style="border-radius: 15px; background-color: white; box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1)"
            elevation="0"
          >
            <v-card-text class="pa-0">
              <!-- Desktop Table View -->
              <div class="agenda-table-wrapper">
                <v-table
                  class="d-none d-md-table google-font agenda-table"
                  style="background-color: transparent"
                >
                  <thead>
                    <tr class="agenda-table-header">
                      <th class="text-left pa-4 agenda-header-cell">
                        Time
                      </th>
                      <th class="text-left pa-4 agenda-header-cell">
                        Session Title
                      </th>
                      <th class="text-left pa-4 agenda-header-cell">
                        Speaker(s)
                      </th>
                      <th class="text-left pa-4 agenda-header-cell">
                        Details
                      </th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      v-for="(session, index) in agendaData"
                      :key="index"
                      class="agenda-table-row"
                      :class="{
                        'agenda-row-highlight': session.highlight,
                        'agenda-row-break': session.isBreak,
                      }"
                    >
                      <td class="pa-4 agenda-time-cell">
                        {{ session.time }}
                      </td>
                      <td class="pa-4 agenda-title-cell">
                        <div v-html="session.title" class="agenda-title-text"></div>
                      </td>
                      <td class="pa-4 agenda-speaker-cell">
                        <div v-html="formatSpeakers(session.speakers)" class="agenda-speaker-text"></div>
                      </td>
                      <td class="pa-4 agenda-details-cell">
                        {{ session.details }}
                      </td>
                    </tr>
                  </tbody>
                </v-table>
              </div>

              <!-- Mobile Card View -->
              <div class="d-md-none">
                <v-card
                  v-for="(session, index) in agendaData"
                  :key="index"
                  class="ma-3 agenda-card"
                  :class="{
                    'agenda-card-highlight': session.highlight,
                    'agenda-card-break': session.isBreak,
                  }"
                  style="border-radius: 12px"
                  elevation="1"
                >
                  <v-card-text class="pa-4">
                    <div class="mb-3">
                      <v-chip
                        size="small"
                        :color="session.isBreak ? 'yellow' : 'primary'"
                        variant="flat"
                        class="google-font"
                        style="font-weight: 700"
                      >
                        {{ session.time }}
                      </v-chip>
                    </div>
                    <h3
                      class="google-font mb-2"
                      style="font-weight: 600; color: #1e1e1e; font-size: 1.1em"
                      v-html="session.title"
                    ></h3>
                    <div
                      v-if="session.speakers && session.speakers !== '–'"
                      class="mb-2 agenda-card-speakers"
                      style="color: #424242"
                    >
                      <strong>Speaker(s):</strong>
                      <div
                        v-html="formatSpeakers(session.speakers)"
                        class="google-font mt-1"
                        style="line-height: 1.6"
                      ></div>
                    </div>
                    <p
                      class="google-font mb-0"
                      style="color: #616161; line-height: 1.6; font-size: 0.95em"
                    >
                      {{ session.details }}
                    </p>
                  </v-card-text>
                </v-card>
              </div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </NuxtLayout>
</template>

<script setup>
const { mainData, scheduleData } = useJSONData();

// Function to format speakers as pill-shaped badges with light background
// This function wraps speaker names in oval-shaped badges using string manipulation
const formatSpeakers = (speakersHtml) => {
  if (!speakersHtml || speakersHtml === '–' || speakersHtml === '-') {
    return speakersHtml;
  }
  
  // Skip formatting if it's already a workshop branch structure
  if (speakersHtml.includes('workshop-branch')) {
    return speakersHtml;
  }
  
  let formatted = speakersHtml;
  
  // Handle speakers with both <strong> and <em> tags together
  // Pattern: <strong>Name</strong> <em>(Details)</em>
  formatted = formatted.replace(/<strong>([^<]+)<\/strong>\s*(<em>[^<]+<\/em>)/g, (match, name, emTag) => {
    if (name.trim() !== 'Track Leads:') {
      return `<span class="speaker-pill"><strong>${name}</strong> ${emTag}</span>`;
    }
    return match;
  });
  
  // Wrap remaining <strong> tags (without following <em>) with pill badges
  formatted = formatted.replace(/<strong>([^<]+)<\/strong>/g, (match, name) => {
    // Skip if already inside a pill badge
    if (!match.includes('speaker-pill') && name.trim() !== 'Track Leads:') {
      return `<span class="speaker-pill"><strong>${name}</strong></span>`;
    }
    return match;
  });
  
  // Handle list items with bullet points (for workshops)
  // Match "• Name – Description" pattern and wrap name in pill
  formatted = formatted.replace(/•\s*([^–<]+?)(?:\s*–|$)/g, (match, name) => {
    const cleanName = name.trim();
    if (cleanName && !cleanName.includes('speaker-pill')) {
      return `• <span class="speaker-pill">${cleanName}</span>`;
    }
    return match;
  });
  
  // Handle plain text speakers (no HTML tags, no bullets)
  // Only if the entire content is plain text
  if (!formatted.includes('<') && !formatted.includes('•') && formatted.trim() && formatted.trim() !== '–') {
    formatted = `<span class="speaker-pill">${formatted}</span>`;
  }
  
  return formatted;
};

// Agenda data with all session details
const agendaData = ref([
  {
    time: "09:30 AM – 10:30 AM",
    title: "Entry & Welcome Ceremony",
    speakers: "GDG Prayagraj Team",
    details: "Participant registration, welcome address, and networking.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "10:30 AM – 11:00 AM",
    title: "Cake Cutting Ceremony",
    speakers: "–",
    details: "Celebration of DevFest spirit with community members.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "11:00 AM – 11:30 AM",
    title: "Keynote Session",
    speakers: "–",
    details: "Opening keynote to kick off DevFest Prayagraj 2025.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "11:30 AM – 12:00 PM",
    title: "Speaker Talk 1: Open Source",
    speakers: "<strong>Praveen Das</strong>",
    details: "Empowering Developers through Open Source Contributions.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "12:00 PM – 12:30 PM",
    title: "Speaker Talk 2: Gemini CLI & MCP Server",
    speakers: "<strong>Anubhav Singh</strong>",
    details: "Exploring the Power of Gemini CLI with MCP Server.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "12:30 PM – 01:00 PM",
    title: "Speaker Talk 3: ADK & Developer Tools",
    speakers: "<strong>Pankaj Rai</strong> <em>(GDE – Firebase)</em>",
    details: "Advanced Developer Kit and Productivity with Firebase Tools.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "01:00 PM – 01:45 PM",
    title: "Speaker Talk 4: Firebase & Cloud",
    speakers: "<strong>Vrijraj Singh</strong> <em>(GDE – Firebase & Web)</em>",
    details: "Scaling Web Apps with Firebase and Google Cloud.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "01:45 PM – 02:00 PM",
    title: "Speaker Talk 5: Cloud Innovations <em>(Tentative)</em>",
    speakers: "<strong>Saurabh Mishra</strong>",
    details: "Next-Gen Cloud Solutions and Deployment Strategies.",
    highlight: false,
    isBreak: false,
  },
  {
    time: "02:00 PM – 03:00 PM",
    title: "Lunch & Networking Break",
    speakers: "–",
    details: "Relax, recharge, and connect with other developers and speakers.",
    highlight: false,
    isBreak: true,
  },
  {
    time: "03:00 PM – 04:00 PM",
    title: "Hands-On Parallel Workshops",
    speakers:
      "<div class='workshop-branch'><div class='branch-header'><strong>Track Leads:</strong></div><div class='branch-list'><div class='branch-item'>Nitin Tiwari – Gemini & Generative AI</div><div class='branch-item'>Saurabh Mishra – Cloud</div><div class='branch-item'>Vrijraj Singh – Firebase</div><div class='branch-item'>Pankaj Rai – Mobile Development</div><div class='branch-item'>Praveen Das – Open Source</div></div></div>",
    details:
      "Deep-dive sessions on modern technologies guided by industry experts.",
    highlight: false,
    isBreak: false,
  },
]);

definePageMeta({
  layout: false,
});

useSeoMeta({
  contentType: "text/html; charset=utf-8",
  title: "Agenda - " + mainData.eventInfo.name + " | " + mainData.communityName,
  description: mainData.eventInfo.description.short,
  keywords: mainData.seo.keywords,
  ogLocale:'en_US',
  author: "GDG Prayagraj Team",
  creator: "GDG Prayagraj Team",
  viewport: "width=device-width, initial-scale=1.0",
  ogTitle:
    "Agenda - " + mainData.eventInfo.name + " | " + mainData.communityName,
  ogDescription: mainData.eventInfo.description.short,
  ogImage: `${mainData.seo.hostUrl}/thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  ogUrl: mainData.seo.hostUrl,
  ogType: "website",
  twitterTitle:
    "Agenda - " + mainData.eventInfo.name + " | " + mainData.communityName,
  twitterDescription: mainData.eventInfo.description.short,
  twitterImage: `${mainData.seo.hostUrl}thumbnail.png?auto=format&fit=crop&frame=1&h=512&w=1024`,
  twitterCard: "summary_large_image",
});
</script>
<style scoped>
/* Page title styling - large, bold, dark grey */
.agenda-page-title {
  font-size: 2.5em;
  font-weight: 700;
  color: #1e1e1e;
  margin-bottom: 16px;
  line-height: 1.2;
}

/* Page description styling - lighter grey */
.agenda-page-description {
  font-size: 1em;
  color: #616161;
  line-height: 1.6;
  max-width: 90%;
}

/* Agenda container styling */
.agenda-container {
  overflow-x: auto;
  border: none;
}

/* Table wrapper for proper spacing */
.agenda-table-wrapper {
  overflow-x: auto;
}

/* Table styling */
.agenda-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
}

/* Table header styling - light grey background */
.agenda-table-header {
  background-color: #f5f5f5 !important;
}

.agenda-header-cell {
  font-weight: 700;
  font-size: 1.05em;
  color: #1e1e1e;
  background-color: #f5f5f5;
  border-bottom: 2px solid #e0e0e0;
  padding: 16px 20px !important;
  text-align: left;
}

/* Table row styling */
.agenda-table-row {
  background-color: white;
  transition: background-color 0.2s ease;
}

.agenda-table-row:hover {
  background-color: #fafafa;
}

/* Highlighted row - yellow background with left border */
.agenda-row-highlight {
  background-color: #fff9e6 !important;
  border-left: 4px solid #fbbc04 !important;
  position: relative;
}

.agenda-row-highlight:hover {
  background-color: #fff5cc !important;
}

/* Break row - distinct grey background with left border */
.agenda-row-break {
  background-color: #f5f5f5 !important;
  border-left: 4px solid #9e9e9e !important;
  font-style: italic;
}

.agenda-row-break:hover {
  background-color: #eeeeee !important;
}

/* Break row text styling */
.agenda-row-break td {
  color: #616161 !important;
}

/* Table cell styling */
.agenda-table-row td {
  border-bottom: 1px solid #f0f0f0;
  padding: 16px 20px !important;
  vertical-align: top;
}

/* Remove bottom border from last row */
.agenda-table-row:last-child td {
  border-bottom: none;
}

/* Time cell - bold styling for better visibility */
.agenda-time-cell {
  font-weight: 700;
  color: #1e1e1e;
  font-size: 0.95em;
  white-space: nowrap;
}

/* Title cell */
.agenda-title-cell {
  font-weight: 500;
}

.agenda-title-text {
  color: #1e1e1e;
  font-size: 0.95em;
  line-height: 1.5;
}

/* Speaker cell */
.agenda-speaker-cell {
  color: #424242;
}

.agenda-speaker-text {
  color: #424242;
  line-height: 1.6;
  font-size: 0.95em;
}

/* Details cell */
.agenda-details-cell {
  color: #616161;
  line-height: 1.6;
  font-size: 0.9em;
}

/* Mobile card styling */
.agenda-card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  margin-bottom: 12px;
}

.agenda-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1) !important;
}

.agenda-card-highlight {
  border-left: 4px solid #fbbc04;
  background-color: #fff9e6;
}

.agenda-card-break {
  border-left: 4px solid #9e9e9e;
  background-color: #f5f5f5;
}

/* Break card text styling */
.agenda-card-break .v-card-text {
  color: #616161;
  font-style: italic;
}

/* HTML content styling within agenda */
.agenda-container :deep(strong) {
  font-weight: 600;
  color: #1e1e1e;
}

.agenda-container :deep(em) {
  font-style: italic;
  color: #616161;
  font-size: 0.9em;
  font-weight: 400;
}

.agenda-container :deep(br) {
  line-height: 1.8;
}

/* Speaker pill badge styling - plain text without background */
.agenda-container :deep(.speaker-pill) {
  display: inline;
  padding: 0;
  background-color: transparent;
  border-radius: 0;
  font-size: 0.9em;
  margin: 0;
  line-height: 1.4;
  color: #424242;
  font-weight: 500;
  transition: none;
  box-shadow: none;
}

/* Hover effect for speaker pills - removed */
.agenda-container :deep(.speaker-pill:hover) {
  background-color: transparent;
  transform: none;
  box-shadow: none;
}

/* Strong tags inside speaker pills */
.agenda-container :deep(.speaker-pill strong) {
  font-weight: 600;
  color: #1a1a1a;
}

/* Em tags inside speaker pills */
.agenda-container :deep(.speaker-pill em) {
  font-style: italic;
  color: #616161;
  font-size: 0.85em;
  font-weight: 400;
}

/* Speaker pills in mobile view - plain text without background */
.agenda-card-speakers :deep(.speaker-pill) {
  display: inline;
  padding: 0;
  background-color: transparent;
  border-radius: 0;
  font-size: 0.9em;
  margin: 0;
  line-height: 1.4;
  color: #424242;
  font-weight: 500;
  transition: none;
  box-shadow: none;
}

.agenda-card-speakers :deep(.speaker-pill:hover) {
  background-color: transparent;
  transform: none;
  box-shadow: none;
}

.agenda-card-speakers :deep(.speaker-pill strong) {
  font-weight: 600;
  color: #1a1a1a;
}

.agenda-card-speakers :deep(.speaker-pill em) {
  font-style: italic;
  color: #616161;
  font-size: 0.85em;
  font-weight: 400;
}

/* Workshop branch tree structure styling */
.agenda-container :deep(.workshop-branch) {
  position: relative;
  padding-left: 0;
}

.agenda-container :deep(.branch-header) {
  margin-bottom: 8px;
  font-weight: 600;
  color: #1e1e1e;
}

.agenda-container :deep(.branch-list) {
  position: relative;
  padding-left: 20px;
}

/* Create vertical line from header to branches */
.agenda-container :deep(.branch-list::before) {
  content: '';
  position: absolute;
  left: 8px;
  top: 0;
  bottom: 0;
  width: 2px;
  background-color: #e0e0e0;
}

/* Branch items with horizontal lines */
.agenda-container :deep(.branch-item) {
  position: relative;
  padding-left: 20px;
  margin-bottom: 6px;
  color: #424242;
  font-size: 0.9em;
  line-height: 1.5;
}

/* Horizontal line connecting to vertical line */
.agenda-container :deep(.branch-item::before) {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  width: 12px;
  height: 2px;
  background-color: #e0e0e0;
  transform: translateY(-50%);
}

/* Small circle at connection point */
.agenda-container :deep(.branch-item::after) {
  content: '';
  position: absolute;
  left: 8px;
  top: 50%;
  width: 6px;
  height: 6px;
  background-color: #9e9e9e;
  border-radius: 50%;
  transform: translate(-50%, -50%);
}

/* Last branch item - no bottom line needed */
.agenda-container :deep(.branch-item:last-child) {
  margin-bottom: 0;
}

/* Mobile view branch styling */
.agenda-card-speakers :deep(.workshop-branch) {
  position: relative;
  padding-left: 0;
}

.agenda-card-speakers :deep(.branch-header) {
  margin-bottom: 8px;
  font-weight: 600;
  color: #1e1e1e;
}

.agenda-card-speakers :deep(.branch-list) {
  position: relative;
  padding-left: 20px;
}

.agenda-card-speakers :deep(.branch-list::before) {
  content: '';
  position: absolute;
  left: 8px;
  top: 0;
  bottom: 0;
  width: 2px;
  background-color: #e0e0e0;
}

.agenda-card-speakers :deep(.branch-item) {
  position: relative;
  padding-left: 20px;
  margin-bottom: 6px;
  color: #424242;
  font-size: 0.9em;
  line-height: 1.5;
}

.agenda-card-speakers :deep(.branch-item::before) {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  width: 12px;
  height: 2px;
  background-color: #e0e0e0;
  transform: translateY(-50%);
}

.agenda-card-speakers :deep(.branch-item::after) {
  content: '';
  position: absolute;
  left: 8px;
  top: 50%;
  width: 6px;
  height: 6px;
  background-color: #9e9e9e;
  border-radius: 50%;
  transform: translate(-50%, -50%);
}

.agenda-card-speakers :deep(.branch-item:last-child) {
  margin-bottom: 0;
}

/* Responsive adjustments */
@media (max-width: 960px) {
  .agenda-page-title {
    font-size: 2em;
  }
  
  .agenda-table {
    font-size: 0.9em;
  }
  
  .agenda-header-cell {
    font-size: 0.95em;
    padding: 12px 16px !important;
  }
  
  .agenda-table-row td {
    padding: 12px 16px !important;
  }
}

/* Remove default Vuetify table borders */
.agenda-table :deep(.v-table) {
  border: none;
}

.agenda-table :deep(.v-table__wrapper) {
  border-radius: 15px;
  overflow: hidden;
}
</style>
