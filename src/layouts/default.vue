<script setup></script>
<template>
  <v-app id="inspire">
    <v-app-bar :elevation="6" color="transparent">
      <v-img
        class="mx-2"
        src="../../public/tarot_icon.png"
        max-height="40"
        max-width="40"
        contain
      ></v-img>
      <v-app-bar-title>Simple Tarot Vue</v-app-bar-title>
      <template v-slot:append>
        <router-link to="/"
          ><v-btn icon="mdi-cards-playing"></v-btn
        ></router-link>

        <router-link to="/historyTarot"
          ><v-btn icon="mdi-clipboard-text-clock"></v-btn
        ></router-link>

        <router-link to="/aboutTarot"
          ><v-btn icon="mdi-information"></v-btn
        ></router-link>
      </template>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
  <v-footer><appFooter /></v-footer>
</template>

<style scoped>
#inspire:before {
  background: url("../images/teatime.jpg");
  background-size: cover;
  height: 100%;
  content: " ";
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  background-position: 50% 0;
  opacity: 0.3;
}
</style>
