<template>
    <div class="cita" :style="{ backgroundColor: colorGravedad }">
        <h3><strong>Paciente:</strong> {{ cita.paciente }}</h3>
      <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
      <p><strong>Hora:</strong> {{ cita.hora }}</p>
      <p><strong>Gravedad:</strong> {{ cita.gravedad }}</p>
      <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
      <button @click="eliminarCita">Eliminar</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Cita',
    props: {
      cita: {
        type: Object,
        required: true
      }
    },
    computed: {
      colorGravedad() {
        switch (this.cita.gravedad) {
          case 'Baja':
            return '#90EE90' // Verde claro
          case 'Media':
            return '#FFFFE0' // Amarillo claro
          case 'Alta':
            return '#FFB6C1' // Rojo claro
          default:
            return 'white'
        }
      }
    },
    methods: {
      eliminarCita() {
        this.$emit('eliminar-cita')
      }
    }
  }
  </script>
  
  <style scoped>
  .cita {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 15px;
    margin-bottom: 15px;
  color: black; /* Asegura que el texto sea negro */
  text-align: left; /* Alinea el texto a la izquierda */
  }
  
  button {
    background-color: #f44336;
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
    margin-top: 10px;
  }
  </style>