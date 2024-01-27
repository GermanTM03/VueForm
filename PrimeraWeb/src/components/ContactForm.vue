<template>
    <form class="my-form" @submit.prevent="submitForm">
      <label for="name">Nombre:</label>
      <input v-model="formData.name" type="text" id="name" :class="{ 'error': errors.name }" />
      <span v-if="errors.name" class="error-message">Ingrese un nombre válido (entre 5 y 18 caracteres)</span>
  
      <label for="apellido">Apellido:</label>
      <input v-model="formData.apellido" type="text" id="apellido" :class="{ 'error': errors.apellido }" />
      <span v-if="errors.apellido" class="error-message">Ingrese un apellido válido (no igual al nombre)</span>
  
      <label for="edad">Edad:</label>
      <input v-model="formData.edad" type="number" id="edad" :class="{ 'error': errors.edad }" />
      <span v-if="errors.edad" class="error-message">Ingrese una edad válida (mayor a 0 y menor a 60)</span>
  
      <label for="genero">Género:</label>
      <select v-model="formData.genero" id="genero" @change="handleGeneroChange" :class="{ 'error': errors.genero }">
        <option value="Masculino">Masculino</option>
        <option value="Femenino">Femenino</option>
        <option value="Otro">Otro</option>
      </select>
      <span v-if="errors.genero" class="error-message">Seleccione un género válido</span>
  
      <!-- Campo adicional para el género personalizado -->
      <input v-if="formData.genero === 'Otro'" v-model="formData.otroGenero" type="text" placeholder="Especificar otro género" />
  
      <button type="submit">Enviar</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          name: '',
          apellido: '',
          edad: '',
          genero: '',
          otroGenero: '', 
        },
      };
    },
    computed: {
      errors() {
        const errors = {};
        if (!this.formData.name.trim() || this.formData.name.length < 5 || this.formData.name.length > 18) {
          errors.name = true;
        }
        if (!this.formData.apellido.trim() || this.formData.apellido === this.formData.name) {
          errors.apellido = true;
        }
        if (!this.formData.edad || isNaN(this.formData.edad) || this.formData.edad <= 0 || this.formData.edad >= 60) {
          errors.edad = true;
        }
        if (!this.formData.genero) {
          errors.genero = true;
        }
        return errors;
      },
    },
    methods: {
      submitForm() {
        // Check for errors before submitting the form
        if (Object.values(this.errors).some(error => error)) {
          // Display error message or take appropriate action
          alert('Por favor, corrija los errores en el formulario.');
        } else {
          // For demonstration purposes, alert "registrado"
          alert('Registrado');
        }
      },
      handleGeneroChange() {
        this.formData.otroGenero = '';
      },
    },
  };
  </script>
  
  <style scoped>
  /* Estilos específicos del componente, con el modificador "scoped" */
  .my-form {
    max-width: 400px;
    margin: auto;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input,
  select {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    box-sizing: border-box;
  }
  
  .error {
    border: 1px solid red;
  }
  
  .error-message {
    color: red;
  }
  
  button {
    background-color: #4caf50;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049;
  }
  </style>
  