<template>
  <v-app class="app">
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-card-text>
          <h4 class="m-0" style="font-family: 'Poppins'">MovieInfo</h4>
        </v-card-text>
      </div>

      <v-spacer></v-spacer>

      <!-- <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn> -->
    </v-app-bar>

    <v-main>
      <lastest-movie />
    </v-main>
  </v-app>
</template>

<script>
import LastestMovie from './components/LatestMovie.vue'
export default {
  name: 'App',

  components: {
    LastestMovie,
  },

  data: () => ({
    //
  }),
};
</script>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

.app {
  font-family: 'Poppins';
}
</style>
