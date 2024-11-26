<template>
    <form @submit.prevent="enviarCita">
      <div v-for="campo in campos" :key="campo.nombre">
        <label :style="{ color: !campo.valor ? 'red' : 'black' }">
          {{ campo.label }}
        </label>
        <input 
          v-model="campo.valor" 
          type="text" 
          :placeholder="campo.label" 
          @input="validarFormulario" 
        />
      </div>
  
      <label>
        Gravedad
      </label>
      <select v-model="gravedad" @change="validarFormulario">
        <option value="" disabled>Seleccione una opción</option>
        <option value="Baja">Baja</option>
        <option value="Media">Media</option>
        <option value="Alta">Alta</option>
      </select>
  
      <button :disabled="!formularioValido">Agregar</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        campos: [
          { nombre: 'paciente', label: 'Paciente', valor: '' },
          { nombre: 'fecha', label: 'Fecha', valor: '' },
          { nombre: 'hora', label: 'Hora', valor: '' },
          { nombre: 'motivo', label: 'Motivo', valor: '' },
        ],
        gravedad: '',
        formularioValido: false,
      };
    },
    methods: {
      validarFormulario() {
        this.formularioValido = this.campos.every((campo) => campo.valor) && this.gravedad;
      },
      enviarCita() {
        const nuevaCita = {
          paciente: this.campos.find((c) => c.nombre === 'paciente').valor,
          fecha: this.campos.find((c) => c.nombre === 'fecha').valor,
          hora: this.campos.find((c) => c.nombre === 'hora').valor,
          motivo: this.campos.find((c) => c.nombre === 'motivo').valor,
          gravedad: this.gravedad,
        };
        this.$emit('agregar-cita', nuevaCita);
        this.limpiarFormulario();
      },
      limpiarFormulario() {
        this.campos.forEach((campo) => (campo.valor = ''));
        this.gravedad = '';
        this.formularioValido = false;
      },
    },
  };
  </script>
  