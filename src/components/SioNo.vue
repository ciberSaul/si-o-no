<template>
  <img src="https://via.placeholder.com/250" alt="fondo">
  <!-- Fondo que oscurece toda la pantalla -->
  <div class="bg-dark"></div>
  <div class="indecision-container">
    <input type="text" placeholder="¿Qué quieres saber?" v-model="pregunta">
    <p>Recuerda terminar con un signo de interrogación (?).</p>
    <div>
      <h2>{{ pregunta }}</h2>
      <h1>Sí, No, Pensando...</h1>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      pregunta: ''

    }
  },
  methods: {
    async obtenerRespuesta() {
      this.respuesta = 'Pensando...';
      const { answer, image } = await fetch('https://yesno.wtf/api').then(respuesta => respuesta.json());
      this.respuesta = answer;
      this.urlImg = image;
    }
  },
  watch: {
    pregunta(valor) {
      this.preguntaCorrecta = false
      if (!valor.includes('?')) return
      this.preguntaCorrecta = true
      this.obtenerRespuesta();
    }
  }
}
</script>