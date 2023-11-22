<template>
  <div class="container">
    <div class="eventos">
      <h2>Eventos Recebidos:</h2>
      <button @click="getTarefas">tesqte</button>
      <div>{{ message }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: [],
    };
  },
  methods: {
    async getTarefas() {
      try {
        const response = await fetch("http://localhost:4000/get/tarefas");
        this.message = await response.json();
        console.log(this.message);
      } catch (error) {
        console.error(error);
      }
    },
    mounted() {
      this.getTarefas();
    },
  },
};
</script>

<style scoped>
* {
  color: black;
}
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
.tes {
  background-color: red;
}
button {
  color: white;
}
</style>
