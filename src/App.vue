<template>
  <v-app>
    <v-content>
      <Main />
      <v-dialog v-model="loading.estado" hide-overlay persistent width="300">
        <v-card :color="loading.color" dark>
          <v-card-text>
            {{ loading.titulo }}
            <v-progress-linear indeterminate color="white" class="mb-0"></v-progress-linear>
          </v-card-text>
        </v-card>
      </v-dialog>
    </v-content>
  </v-app>
</template>

<script>
import Main from "./components/Main";
import { mapState } from 'vuex';

export default {
  name: "App",
  components: {
    Main
  },
  computed: {
    ...mapState(['loading'])
  }
};
</script>
