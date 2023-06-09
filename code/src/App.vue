<template>
  <div id="app">
    <header class="header bg-secondary mb-4"></header>
    <BestTransport />
  </div>
</template>

<script>
import BestTransport from "./components/BestTransport.vue";

export default {
  name: "App",
  components: {
    BestTransport
  }
};
</script>

<style lang="scss">
@import "assets/scss/theme.scss";

body {
  font-family: "Montserrat";
  font-weight: 400;
}

.btn {
  font-weight: 600;
}

.header {
  width: 100%;
  height: 50px;
}
</style>
