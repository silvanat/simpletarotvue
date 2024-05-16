<template>
  <v-container class="fill-height align-content-start">
    <v-card class="mx-auto vcard" prepend-icon="mdi-information">
      <template v-slot:title>
        <span class="font-weight-black">About Simple Tarot Vue APP</span>
      </template>

      <v-card-text class="bg-surface-light pt-4">
        <p class="mb-6 mt-6">
          This project was created with Vuetify 3 for learning purposes.
        </p>
        <p class="mb-6">
          This project consume the
          <a href="https://tarotapi.dev/">Tarot API.</a>
        </p>
        <p class="mb-6">
          Github:
          <a href="https://github.com/silvanat/simpletarotvue" target="_blank"
            >https://github.com/silvanat/simpletarotvue</a
          >
        </p>

        <p class="mb-6">
          Publication:
          <a href="https://simpletarot-vue.netlify.app" target="_blank"
            >https://simpletarot-vue.netlify.app</a
          >
        </p>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script setup>
//
</script>
<style>
.vcard {
  width: 100%;
}
</style>
