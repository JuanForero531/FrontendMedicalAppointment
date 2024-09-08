<template>
    <div id="cancelar-cita">
      <h2>Cancelar Cita</h2>
      <form @submit.prevent="cancelarCita">
        <label for="codigo">Código de la Cita:</label>
        <input type="text" v-model="codigo" required>
  
        <button type="submit">Cancelar Cita</button>
      </form>
      <div v-if="mensajeCancelacion">{{ mensajeCancelacion }}</div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        codigo: '',
        mensajeCancelacion: ''
      };
    },
    methods: {
      async cancelarCita() {
        try {
          await axios.delete(`http://localhost:3000/appointments/${this.codigo}`);
          this.mensajeCancelacion = 'Cita cancelada exitosamente.';
        } catch (error) {
          console.error('Error al cancelar la cita:', error);
          this.mensajeCancelacion = 'Error al cancelar la cita.';
        }
      }
    }
  };
  </script>
  