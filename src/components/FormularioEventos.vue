<template>
  <div>
    <h2>Formulário do Evento</h2>
    <form @submit.prevent="enviarFormulario">
      <div>
        <label for="nome">Nome do Evento:</label>
        <input type="text" id="nome" v-model="evento.nome" required>
      </div>
      <div>
        <label for="data">Data do Evento:</label>
        <input type="date" id="data" v-model="evento.data" required>
      </div>
      <div>
        <label for="categoria">Categoria:</label>
        <input type="text" id="categoria" v-model="evento.categoria" required>
      </div>
      <div>
        <label for="cor">Cor:</label>
        <select id="cor" v-model="evento.cor" required>
          <option value="vermelho">Vermelho</option>
          <option value="azul">Azul</option>
          <option value="verde">Verde</option>
          <option value="amarelo">Amarelo</option>
        </select>
      </div>
      <button type="submit">Enviar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      evento: {
        nome: '',
        data: '',
        categoria: '',
        cor: '', 
      },
    };
  },
  methods: {
    enviarFormulario() {
      // Emitir o evento enviarDados com os dados do evento
      this.$emit('enviarDados', this.evento);

      // Restante do código para download do JSON (se necessário)
      const dadosJSON = JSON.stringify(this.evento, null, 2);
      const blob = new Blob([dadosJSON], { type: 'application/json' });
      const link = document.createElement('a');
      link.href = window.URL.createObjectURL(blob);
      link.download = 'dados_evento.json';
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);

      console.log('Enviando dados:', this.evento);
    },
  },
};
</script>

<style scoped>
/* Adicione estilos específicos para este componente se necessário */
</style>
