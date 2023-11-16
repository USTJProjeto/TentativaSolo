<template>
  <div>
    <FormularioEvento @enviarDados="receberDados" />
    <ComponenteOutro :eventos="listaEventos" />
  </div>
</template>

<script>
import FormularioEvento from './components/FormularioEventos.vue';
import ComponenteOutro from './components/ComponenteOutro.vue';

export default {
  components: {
    FormularioEvento,
    ComponenteOutro,
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
