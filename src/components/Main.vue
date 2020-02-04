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
            :max="maximo"
            @change="getDolar(fecha)">
          </v-date-picker>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-center">{{ valor }}</v-card-text>
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
          fecha: new Date().toISOString().substr(0, 10),
          minimo: '1984',
          maximo: new Date().toISOString().substr(0, 10),
          valor: null
      }
  },
  methods: {
      async getDolar(dia) {
          let arrayFecha = dia.split(['-']);
          let ddmmyy =`${arrayFecha[2]}-${arrayFecha[1]}-${arrayFecha[0]}`;

          try {
            let datos = await axios.get(`https://mindicador.cl/api/dolar/${ddmmyy}`);
            console.log(datos.data.serie);
            if (datos.data.serie.length > 0) {
                this.valor = datos.data.serie[0].valor;
            } else {
                this.valor = 'Sin resultados';
            }
          } catch (error) {
              console.log('Error axios');
          } finally {

          }
      }
  },
  created() {
      this.getDolar(this.fecha);
  }
}
</script>