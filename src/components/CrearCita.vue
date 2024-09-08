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
      <div v-if="codigoCita">Código de la cita: {{ codigoCita }}</div>
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
        codigoCita: ''
      };
    },
    methods: {
      onFileChange(event) {
        this.autorizacion = event.target.files[0];
      },
      async crearCita() {
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
        } catch (error) {
          console.error('Error al crear la cita:', error);
        }
      }
    }
  };
  </script>
  