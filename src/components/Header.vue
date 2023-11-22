<template>
  <header class="custom-header">
    <img src="../assets/logo.svg" />
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
header {
  margin: 0 auto;
  width: 100%;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}
header img {
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
