<template>
  <div class="container">
    <div class="formulario">
      <h2>Criação de tarefa</h2>
      <form method="post" action="http://localhost:4000/post/tarefas">
        <div class="first-component">
          <div class="campo-formulario">
            <label for="nome">Nome do Evento:</label>
            <input type="text" name="nome" v-model="form.nome" required />
          </div>
          <div class="campo-formulario">
            <label for="data">Data do Evento:</label>
            <input type="date" name="data" v-model="form.data" required />
          </div>
        </div>
        <div class="second-component">
          <div class="campo-formulario">
            <label for="categoria">Categoria:</label>
            <input
              type="text"
              name="categoria"
              v-model="form.categoria"
              required
            />
          </div>
          <div class="campo-formulario">
            <label for="cor">Cor:</label>
            <input
              class="input-color"
              type="color"
              id="head"
              name="cor"
              value="#e66465"
            />
          </div>
        </div>
        <div class="third-component">
          <div class="campo-formulario">
            <label for="categoria">Descrição:</label>
            <input
              type="text"
              name="descricao"
              v-model="form.descricao"
              required
            />
          </div>
        </div>
        <div class="button-component">
          <button type="submit" class="botao-enviar">Criar</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        nome: "",
        data: "",
        categoria: "",
        cor: "",
        descricao: "",
      },
    };
  },
  methods: {
    async submit() {
      this.$emit("submit", this.form);
    },
  },
};
</script>

<style scoped>
.botao-enviar{
    background-color: #FF3366;
}
.input-color {
  height: 35px;
  width: 35px !important;
}
label {
  font-weight: 700;
}
h2 {
  color: white;
}
* {
  color: black;
}
.container {
  display: flex;
}

.formulario {
    width: 100%;
    height: 25em;
    padding: 20px;
    background-color: #333333;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.campo-formulario {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  color: white;
}

input,
select {
  min-width: 400px;
  padding: 8px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: white;
}

button {
  background-color: #3498db;
  color: #fff;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #007bb5;
}

.first-component,
.second-component {
  display: flex;
  flex-direction: row;
  gap: 0.8em;
}
.third-component {
  display: flex;
  flex-direction: flex-start;
  width: 200px;
}
.button-component {
  display: flex;
  justify-content: flex-end;
}
</style>
