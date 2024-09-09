<template>
  <div id="crear-cita">
    <h2>Crear Cita Médica</h2>
    <form @submit.prevent="crearCita">
      <label for="cc">CC del paciente:</label>
      <input type="text" v-model="cc" required>

      <label for="fecha">Fecha de la cita:</label>
      <input type="date" v-model="fecha" required>

      <label for="autorizacion">Copia de la Autorización (Foto):</label>
      <input type="file" @change="onFileChange" accept="image/*" required>

      <button type="submit">Crear Cita</button>
    </form>
    
    <div v-if="codigoCita" class="success">
      <p>Cita creada con éxito. Código de la cita: {{ codigoCita }}</p>
    </div>
    
    <div v-if="mensajeExito" class="success">
      <p>{{ mensajeExito }}</p>
    </div>

    
    <div v-if="mensajeError" class="error">
      <p>{{ mensajeError }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      cc: '',
      fecha: '',
      autorizacion: null,
      codigoCita: '',
      mensajeExito: '',  
      mensajeError: ''   
    };
  },
  methods: {
    onFileChange(event) {
      this.autorizacion = event.target.files[0];
    },
    async crearCita() {
      console.log("Enviando datos al backend...");
      const formData = new FormData();
      formData.append('cc', this.cc);
      formData.append('date', this.fecha);
      formData.append('authorization', this.autorizacion);

      try {
        const response = await axios.post('http://localhost:3000/appointments', formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        });

        
        this.codigoCita = response.data.code;

        alert('Cita creada\nCódigo de cita: ' + response.data.code);
        this.mensajeError = ""; 

      } catch (error) {
        this.mensajeExito = "";
        if (error.response) {
          this.mensajeError = error.response.data.message;
          console.log('Error al crear la cita:', this.mensajeError);
        } else {
          this.mensajeError = 'Error de red o de servidor al crear la cita';
          console.log('Error al crear la cita:', this.mensajeError);
        }
      }
    }
  }
};
</script>

<style>
.success {
  color: green;
  margin-top: 10px;
}

.error {
  color: red;
  margin-top: 10px;
}
</style>
