<template>
  <div class="container">
    <div class="eventos">
      <h2>Tarefas</h2>
      <div class="btn-ctn">
        <button @click="fetchData">Ver Tarefas</button>
        <button id="myBtn" @click="btnClick">Ver Lembretes</button>
      </div>
      <div id="myModal" class="modal">
        <!-- Modal content -->
        <div class="modal-content">
          <span @click="spanClick" class="close">&times;</span>
          <div class="modal-form-container">
            <div class="frex">
              <h2>Lembretes Diários</h2>
              <button @click="fetchTwoData">Reload</button>
              <div class="container-p-for">
                <p
                  class="badge"
                  :style="{ backgroundColor: lembrete.lembrete.cor }"
                  v-for="lembrete in lembreteData"
                >
                  {{ lembrete.lembrete.lembrete }} #{{ lembrete.id }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="container-table">
        <table class="table">
          <thead>
            <th>Tarefa</th>
            <th>Data</th>
            <th>Categoria</th>
            <th>Descrição</th>
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
              <td>{{ tarefa.tarefa.categoria }}</td>
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
      lembreteData: null,
      dataLoaded: false,
      selectedTarefaId: null,
    };
  },
  methods: {
    btnClick() {
      var modal = document.getElementById("myModal");
      var btn = document.getElementById("myBtn");
      var span = document.getElementsByClassName("close")[0];
      modal.style.display = "block";
    },
    spanClick() {
      var modal = document.getElementById("myModal");
      var btn = document.getElementById("myBtn");
      var span = document.getElementsByClassName("close")[0];
      modal.style.display = "none";
    },
    windowClick() {
      if (event.target == modal) {
        modal.style.display = none;
      }
    },
    fetchData() {
      axios
        .get("http://localhost:4000/get/tarefas")
        .then((response) => {
          this.tarefaData = response.data;
          this.dataLoaded = false;
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    },
    fetchTwoData() {
      axios
        .get("http://localhost:5000/get/lembrete")
        .then((response) => {
          this.lembreteData = response.data;
          this.dataLoaded = false;
          console.log(lembreteData);
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    },
  },
  mounted() {
    this.fetchTwoData();
    this.fetchData();
  },
};
</script>

<style scoped>
.container-p-for {
  display: flex;
  flex-direction: column;
}
.botao-enviar-anotacao {
  margin-top: 10px;
  background-color: pink;
}
.modal-form-container {
  display: flex;
  justify-content: center;
}
form {
  display: flex;
  flex-direction: column;
  width: 100px;
  justify-content: center;
  align-items: center;
}
form input {
}
form input,
select {
  background-color: white;
}
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
  width: 40%;
  border-radius: 0.8em;
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
