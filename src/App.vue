<template>
    <header>
        <Header/>
    </header>
  <div id="main">
    <FormularioEvento @enviarDados="receberDados" />
    <ComponenteOutro :eventos="listaEventos" />
  </div>
</template>

<script>
import FormularioEvento from "./components/FormularioEventos.vue";
import ComponenteOutro from "./components/ComponenteOutro.vue";
import Header from "./components/Header.vue";

export default {
  components: {
    FormularioEvento,
    ComponenteOutro,
    Header,
  },
  data() {
    return {
      listaEventos: [],
    };
  },
  methods: {
    receberDados(dados) {
      // Adicione cada novo evento à lista
      this.listaEventos.push(dados);
    },
  },
};
</script>
