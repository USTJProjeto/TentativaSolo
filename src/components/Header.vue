<template>
  <header class="custom-header">
    <nav>
      <a class="nav-link">Criar Tarefa</a>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.custom-header {
  background-color: #ff66b2; /* Cor rosa */
  height: 100px;
  padding: 10px;
}

.nav-link {
  color: #fff; /* Texto branco */
  margin-right: 15px;
  text-decoration: none;
  font-weight: bold;
}

.nav-link:hover {
  text-decoration: underline;
}
</style>
