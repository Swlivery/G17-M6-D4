<template>
  <div id="app">
    <h1>Administrador de Citas Médicas</h1>
    <FormularioCita @nueva-cita="agregarCita" />
    <div v-if="citas.length === 0" class="sin-citas">
      Aún no hay consultas registradas
    </div>
    <div v-else class="lista-citas">
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
import FormularioCita from './components/FormularioCita.vue'
import Cita from './components/Cita.vue'

export default {
  name: 'App',
  components: {
    FormularioCita,
    Cita
  },
  data() {
    return {
      citas: []
    }
  },
  methods: {
    agregarCita(cita) {
      this.citas.push(cita)
    },
    eliminarCita(index) {
      this.citas.splice(index, 1)
    }
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.sin-citas {
  text-align: center;
  margin-top: 20px;
  font-style: italic;
}

.lista-citas {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  margin-top: 20px;
}
</style>