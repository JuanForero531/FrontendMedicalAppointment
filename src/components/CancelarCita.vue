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
        await axios.delete(`http://localhost:3000/appointments?code=${this.codigo}`);
        this.mensajeCancelacion = 'Cita cancelada exitosamente.';
      } catch (error) {
        if (error.response) {
          this.mensajeCancelacion = error.response.data.message;
          console.log('Error al cancelar cita:', this.mensajeCancelacion);
        } else {
          this.mensajeCancelacion = 'Error de red o de servidor al cancelar cita';
          console.log('Error al cancelar cita:', this.mensajeCancelacion);
        }
      }
    }
  }
};
</script>