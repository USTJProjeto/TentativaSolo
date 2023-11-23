<template>
  <div class="container">
    <div class="eventos">
      <h2>Eventos Recebidos:</h2>
      <button @click="fetchData">Ver Tarefas</button>
      <table class="table">
        <thead>
          <th>Tarefa</th>
          <th>Data</th>
          <th>Categoria</th>
          <th>Descrição</th>
        </thead>
        <tbody>
          <tr v-for="tarefa in responseData">
            <td>{{ tarefa.nome }}</td>
            <td>{{ tarefa.data }}</td>
            <td>{{ tarefa.categoria }}</td>
            <td>{{ tarefa.descricao }}</td>
          </tr>
        </tbody>
      </table>
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
table {
  background-color: red;
}
th {
  text-align: center;
}
td {
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
