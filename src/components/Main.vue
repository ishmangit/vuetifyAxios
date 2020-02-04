<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card class="text-center">
          <v-date-picker
            v-model="fecha"
            full-width
            locale="es"
            :min="minimo"
            :max="maximo">
          </v-date-picker>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-center">{{ valor }} - {{ fecha }}</v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Main',
  data() {
      return {
          fecha: '',
          minimo: '1984',
          maximo: new Date().toISOString().substr(0, 10),
          valor: null
      }
  },
  methods: {
      async getDolar(dia) {
          let datos = await axios.get(`https://mindicador.cl/api/dolar/${dia}`);
          console.log(datos.data.serie[0].valor);
          this.valor = datos.data.serie[0].valor;
      }
  },
  created() {
      this.getDolar('01-02-2019');
  }
}
</script>