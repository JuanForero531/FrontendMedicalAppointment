<template>
    <div id="consultar-citas">
      <h2>Consultar Citas</h2>
      <form @submit.prevent="consultarCitas">
        <label for="fecha-inicio">Fecha Inicio:</label>
        <input type="date" v-model="fechaInicio" required>
  
        <label for="fecha-fin">Fecha Fin:</label>
        <input type="date" v-model="fechaFin" required>
  
        <button type="submit">Consultar Citas</button>
      </form>
      <ul>
        <li v-for="cita in citas" :key="cita.code">
          <p>Código: {{ cita.code }}</p>
          <p>CC: {{ cita.cc }}</p>
          <p>Fecha: {{ cita.date }}</p>
          <img :src="`http://localhost:3000/${cita.authorization}`" alt="Autorización" />
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        fechaInicio: '',
        fechaFin: '',
        citas: []
      };
    },
    methods: {
      async consultarCitas() {
        try {
          const response = await axios.get(`http://localhost:3000/appointments?start=${this.fechaInicio}&end=${this.fechaFin}`);
          this.citas = response.data;
        } catch (error) {
          console.error('Error al consultar las citas:', error);
        }
      }
    }
  };
  </script>
  