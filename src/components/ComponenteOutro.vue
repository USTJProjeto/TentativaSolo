<template>
  <div>
    <h2>Eventos Recebidos:</h2>
    <div v-for="(evento, index) in eventos" :key="index" :style="{ background: evento.cor }">
      <strong>Data do Evento:</strong> {{ evento.data }}
      <br />
      <strong>Categoria:</strong> {{ evento.categoria }}
      <hr />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    eventos: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
/* Adicione estilos específicos para este componente se necessário */
</style>
