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
            <div class="q-gutter-md row items-start">
              <q-input
                filled
                v-model="color"
                class="my-input"
                >
                <template v-slot:append>
                  <q-icon name="colorize" class="cursor-pointer">
                    <q-popup-proxy cover transition-show="scale" transition-hide="scale">
                      <q-color v-model="color" />
                    </q-popup-proxy>
                  </q-icon>
                </template>
              </q-input>

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
.my-input {
  max-width: 250px;
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
  background-color: #ff3366;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.campo-formulario {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input,
select {
  min-width: 100px;
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
