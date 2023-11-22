<template>
  <div class="container">
    <div class="eventos">
      <h2>Eventos Recebidos:</h2>
      <button @click="fetchData">Ver Tarefas</button>
      <div v-for="tarefa in responseData">
        <div class="card">
          <div class="cont card-top">
            <div class="card-nome">
              <p>{{ tarefa.nome }}</p>
            </div>
            <div class="card-data">
              <p>{{ tarefa.data }}</p>
            </div>
          </div>
          <div class="cont card-bottom">
            <div class="card-descricao">
              <p>{{ tarefa.descricao }}</p>
            </div>
            <div class="card-cor">
              <p>{{ tarefa.cor }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      responseData: null,
      dataLoaded: false,
    };
  },
  methods: {
    fetchData() {
      axios
        .get("http://localhost:4000/get/tarefas")
        .then((response) => {
          this.responseData = response.data;
          this.dataLoaded = true;
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    },
  },
};
</script>

<style scoped>
.card {
  background-color: #ff3366;
  margin: 0.8em;
  border-radius: 0.8em;
}
.card-top,
.card-bottom {
  display: flex;
  flex-direction: row;
  gap: 1.2rem;
}
.cont p {
  background-color: white;
  padding: 0.1em;
  border-radius: 0.4em;

}

* {
  color: black;
}
.container {
  display: flex;
}

.eventos {
  flex-grow: 1;
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
