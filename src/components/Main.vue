<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card class="text-center">
          <v-date-picker v-model="fecha" full-width>

          </v-date-picker>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-center">650 - {{ fecha }}</v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Main',
  data() {
      return {
          fecha: ''
      }
  }
}
</script>