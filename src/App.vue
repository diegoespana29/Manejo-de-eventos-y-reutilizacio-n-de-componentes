<template>
  <div>
    <h1>Administrador de Citas Médicas</h1>
    <Formulario @agregar-cita="agregarCita" />
    <div v-if="citas.length === 0" class="no-citas">Aún no hay consultas registradas</div>
    <div v-else>
      <Cita 
        v-for="(cita, index) in citas" 
        :key="index" 
        :cita="cita" 
        @eliminar-cita="eliminarCita(index)" 
      />
    </div>
  </div>
</template>

<script>
import Formulario from './FormularioCitas.vue';
import Cita from './CitaMedica.vue';

export default {
  data() {
    return {
      citas: [],
    };
  },
  methods: {
    agregarCita(nuevaCita) {
      this.citas.push(nuevaCita);
    },
    eliminarCita(index) {
      this.citas.splice(index, 1);
    },
  },
  components: {
    Formulario,
    Cita,
  },
};
</script>
