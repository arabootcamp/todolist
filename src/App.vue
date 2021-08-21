<template>
  <div id="app" class="container h-101">
    <formulario />
  </div>

</template>

<script>
  import Formulario from './components/Formulario.vue';
  export default {
    components: {
      Formulario
    },
    name: "App"
  };
</script>

<style scoped>

.h-101{
  height: calc(100vh + 1px);
}

</style>