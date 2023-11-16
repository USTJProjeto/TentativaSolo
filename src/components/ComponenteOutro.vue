<template>
  <div class="container">
    <div class="eventos">
      <h2>Eventos Recebidos:</h2>
      <div v-for="(evento, index) in eventos" :key="index" class="evento" :style="{ background: evento.cor }">
        <strong>Data do Evento:</strong> {{ evento.data }}
        <br />
        <strong>Categoria:</strong> {{ evento.categoria }}
        <hr />
      </div>
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
.container {
  display: flex;
}

.eventos {
  flex-grow: 1;
  padding: 20px;
}

.evento {
  margin-bottom: 15px;
  padding: 10px;
  border-radius: 4px;
}

</style>
