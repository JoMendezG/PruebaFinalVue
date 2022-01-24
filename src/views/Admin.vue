<template>
  <div>
    <h1 class="display-1 mb-5 mt-5">Administración</h1>
    <tablaCursos></tablaCursos>
  </div>
</template>

<script>
import tablaCursos from "../components/AdminTable.vue";

export default {
  components: {
    tablaCursos,
  },
};
</script>

<style>
h1 {
  text-align: center;
  font-family: "Roboto", sans-serif;
}
</style>
