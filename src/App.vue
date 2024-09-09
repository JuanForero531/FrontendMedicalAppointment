<template>
  <div id="app">
    <header>
    <h1>Gestión de Citas Médicas</h1>
  </header>
    <CrearCita />
    <ConsultarCitas />
    <CancelarCita />
  </div>
</template>
<style>
header {
    background-color: #3498db;
    color: white; 
    padding: 20px;
    text-align: center;
    position: initial; 
    top: 0;
    left: 0;
    width: 100%;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1); 
    z-index: 1000; 
}

main {
    margin-top: 80px; 
}
</style>

<script>
import CrearCita from './components/CrearCita.vue';
import ConsultarCitas from './components/ConsultarCitas.vue';
import CancelarCita from './components/CancelarCita.vue';

export default {
  components: {
    CrearCita,
    ConsultarCitas,
    CancelarCita
  }
};
</script>
