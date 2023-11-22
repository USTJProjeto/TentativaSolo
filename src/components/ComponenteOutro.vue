<template>
  <div class="container">
    <div class="eventos">
      <h2>Eventos Recebidos:</h2>
      <button @click="fetchData">Ver Tarefas</button>
      <div class="container-card">
        <div v-for="tarefa in responseData">
          <div class="card">
              <div class="card-inside">
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
.card-inside{
    background-color: white;
    border-radius: 0.8em;
}
.container-card {
  display: grid;
  column-gap: 0.8em;
  row-gap: 0.8em;
  grid-template-columns: 1fr 1fr;
  margin-top: 0.8em;
}
.card {
  background-color: #ff3366;
  border-radius: 0.8em;
}
.card-top,
.card-bottom {
  display: flex;
  flex-direction: row;
  gap: 1.2rem;
}
.cont p {
  background-color: #ff3366;
  padding: 0.1em;
  border-radius: 0.4em;
  color: white;
  font-weight: 700;
  padding: 0.2em;
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
