<template>
  <div class="container">
    <div class="eventos">
      <h2>Tarefas</h2>
      <button @click="fetchData">Ver Tarefas</button>
      <div class="container-table">
        <table class="table">
          <thead>
            <th>Tarefa</th>
            <th>Data</th>
            <th>Categoria</th>
            <th>Anotação</th>
          </thead>
          <tbody>
            <tr v-for="tarefa in tarefaData">
              <td>{{ tarefa.tarefa.nome }}</td>
              <td>{{ tarefa.tarefa.data }}</td>
              <td class="td-cor">
                <span
                  class="badge"
                  :style="{ backgroundColor: tarefa.tarefa.cor }"
                  >{{ tarefa.tarefa.categoria }}</span
                >
              </td>
              <td>
                {{ tarefa.tarefa.descricao }}
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      tarefaData: null,
      anotacaoData: null,
      dataLoaded: false,
    };
  },
  methods: {
    fetchData() {
      axios
        .get("http://localhost:4000/get/tarefas")
        .then((response) => {
          this.tarefaData = response.data;
          this.dataLoaded = false;

          // Use Promise.all to handle multiple asynchronous requests
          const requests = this.tarefaData.map((tarefa) => {
            return axios.get(
              `http://localhost:5000/get/tarefas/${tarefa.id}/anotacoes`
            );
          });

          return Promise.all(requests);
        })
        .then((anotacoesResponses) => {
          // Handle responses for each anotacoes request
          this.anotacaoData = anotacoesResponses.map(
            (response) => response.data
          );
          this.dataLoaded = true;
          console.log(this.anotacaoData);
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    },
  },
};
</script>

<style scoped>
.badge {
  color: white;
  padding: 4px 8px;
  text-align: center;
  border-radius: 5px;
}
* {
  scroll-behavior: smooth;
}
.container-table {
  margin: 0.8em 0;
}
tr:nth-child(even) {
  background-color: #bababa;
}
table {
  margin: 0 auto;
  min-width: 1280px;
  padding: 10px;
  border-collapse: collapse;
}
th {
  text-align: center;
  background-color: #333333;
  color: white;
  font-weight: 600;
  font-size: 1.4em;
}
td {
  text-align: center;
  padding: 0.5em;
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
