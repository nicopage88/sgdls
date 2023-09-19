<template>
    <div class="hora-fecha-component">
      <h1>Hora y Fecha Actual</h1>
      <p>Fecha: {{ fecha }}</p>
      <p>Hora: {{ hora }}</p>
      <p class="texto-cambiante">{{ textoCambiante }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        fecha: "",
        hora: "",
        textoCambiante: "¡Hola desde mi componente Test, siguamos con este texto, bueno puede sr hasta 2000 caracteres y es estatico de momento...!",
      };
    },
    mounted() {
      this.obtenerFechaHoraActual();
      setInterval(this.obtenerFechaHoraActual, 1000); // Actualizar cada segundo
      
      // Iniciar la animación de texto cada segundo
      setInterval(this.animarTexto, 1000);
    },
    methods: {
      obtenerFechaHoraActual() {
        const ahora = new Date();
        this.fecha = ahora.toLocaleDateString("es-ES");
        this.hora = ahora.toLocaleTimeString("es-ES");
      },
      animarTexto() {
        // Cambiar la posición a la izquierda
        this.textoCambiante = this.textoCambiante.slice(1) + this.textoCambiante[0];
      },
    },
  };
  </script>
  
  <style scoped>
  .hora-fecha-component {
    background-color: black;
    color: white;
    padding: 10px;
    position: relative; /* Añadimos posición relativa */
  }
  
  .texto-cambiante {
    white-space: nowrap; /* Evita que el texto se divida en líneas */
    overflow: hidden; /* Oculta el texto que se desborda */
    width: 200px; /* Establecemos un ancho para el efecto de desplazamiento */
    animation: slideLeft 5s linear infinite; /* Agregamos animación de desplazamiento */
  }
  
  @keyframes slideLeft {
    0% {
      transform: translateX(100%); /* Inicio: completamente desplazado a la derecha */
    }
    100% {
      transform: translateX(-100%); /* Final: completamente desplazado a la izquierda */
    }
  }
  </style>
  