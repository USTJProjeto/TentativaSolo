<template>
  <div class="container">
    <div class="eventos">
      <h2>Tarefas</h2>
      <div class="btn-ctn">
        <button @click="fetchData">Ver Tarefas</button>
        <button id="myBtn" @click="btnClick">Adicionar anotação</button>
      </div>
      <div id="myModal" class="modal">
        <!-- Modal content -->
        <div class="modal-content">
          <span class="close">&times;</span>
          <div class="modal-form-container">
            <form method="post" :action="formSubmit">
              <select name="sel-tarefa" v-model="selectedTarefaId" id="tar">
                <option
                  v-for="tarefa in tarefaData"
                  :key="tarefa.id"
                  :value="tarefa.id"
                >
                  {{ tarefa.tarefa.nome }}
                  {{ tarefa.id }}
                </option>
              </select>
              <label>Anotacão</label>
              <input
                type="anotacao"
                name="anotacao"
                v-model="anotacao"
                required
              />
              <button type="submit" class="botao-enviar">Criar Anotação</button>
            </form>
          </div>
        </div>
      </div>
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
              <td>{{ tarefa.id }}</td>
              <!-- <td v-for="anotacao in anotacaoData"> -->
              <!--     a -->
              <!-- </td> -->
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
      selectedTarefaId: null,
    };
  },
  computed: {
    formSubmit() {
      console.log(this.selectedTarefaId);
      return this.selectedTarefaId;
    },
  },
  methods: {
    btnClick() {
      var modal = document.getElementById("myModal");
      var btn = document.getElementById("myBtn");
      var span = document.getElementsByClassName("close")[0];
      modal.style.display = "block";
    },
    fetchData() {
      axios
        .get("http://localhost:4000/get/tarefas")
        .then((response) => {
          this.tarefaData = response.data;
          this.dataLoaded = false;

          const requests = this.tarefaData.map((tarefa) => {
            return axios.get(
              `http://localhost:5000/get/tarefas/{this.selectedTarefaId}/anotacoes`
            );
          });

          return Promise.all(requests);
        })
        .then((anotacoesResponses) => {
          this.anotacaoData = anotacoesResponses.map(
            (response) => response.data
          );
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
/* The Modal (background) */
.modal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  background-color: #fefefe;
  margin: auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}

/* The Close Button */
.close {
  color: #aaaaaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
.btn-ctn {
  display: flex;
  justify-content: space-between;
}
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
