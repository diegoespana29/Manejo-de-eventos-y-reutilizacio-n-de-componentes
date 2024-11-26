<template>
    <div :style="{ backgroundColor: coloresGravedad[cita.gravedad] }" class="cita-card">
      <h3>{{ cita.paciente }}</h3>
      <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
      <p><strong>Hora:</strong> {{ cita.hora }}</p>
      <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
      <button @click="$emit('eliminar-cita')">Eliminar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cita: Object,
    },
    data() {
      return {
        coloresGravedad: {
          Baja: 'green',
          Media: 'yellow',
          Alta: 'red',
        },
      };
    },
  };
  </script>
  
  <style>
  .cita-card {
    padding: 10px;
    margin: 10px 0;
    border-radius: 5px;
    color: white;
  }
  </style>
  