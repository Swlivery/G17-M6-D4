<template>
<form @submit.prevent="agregarCita">
    <div class="formulario-grid">
      <div class="campo">
        <label :class="{ 'campo-vacio': !cita.paciente }">Paciente:</label>
        <input v-model="cita.paciente" required>
      </div>
      <div class="campo">
        <label :class="{ 'campo-vacio': !cita.fecha }">Fecha:</label>
        <input type="date" v-model="cita.fecha" required>
      </div>
      <div class="campo">
        <label :class="{ 'campo-vacio': !cita.hora }">Hora:</label>
        <input type="time" v-model="cita.hora" required>
      </div>
      <div class="campo">
        <label :class="{ 'campo-vacio': !cita.gravedad }">Gravedad:</label>
        <select v-model="cita.gravedad" required>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
      </div>
      <div class="campo campo-motivo">
        <label :class="{ 'campo-vacio': !cita.motivo }">Motivo:</label>
        <textarea v-model="cita.motivo" required></textarea>
      </div>
    </div>
    <button type="submit" :disabled="!formularioCompleto">Agregar</button>
  </form>
</template>
  
  <script>
  export default {
    name: 'FormularioCita',
    data() {
      return {
        cita: {
          paciente: '',
          fecha: '',
          hora: '',
          gravedad: '',
          motivo: ''
        }
      }
    },
    computed: {
      formularioCompleto() {
        return this.cita.paciente && this.cita.fecha && this.cita.hora && this.cita.gravedad && this.cita.motivo
      }
    },
    methods: {
      agregarCita() {
        if (this.formularioCompleto) {
          this.$emit('nueva-cita', { ...this.cita })
          this.limpiarFormulario()
        }
      },
      limpiarFormulario() {
        this.cita = {
          paciente: '',
          fecha: '',
          hora: '',
          gravedad: '',
          motivo: ''
        }
      }
    }
  }
  </script>
  
  <style scoped>
form {
  margin-bottom: 20px;
}

.formulario-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}

.campo {
  display: flex;
  flex-direction: column;
}

.campo-motivo {
  grid-column: 1 / -1;
}

label {
  margin-bottom: 5px;
}

.campo-vacio {
  color: red;
}

input, select, textarea {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

textarea {
  resize: vertical;
  min-height: 100px;
}

button {
  margin-top: 15px;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}
</style>