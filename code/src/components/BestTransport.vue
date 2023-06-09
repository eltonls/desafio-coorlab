<template>
  <section class="analise-section container rounded-bottom">
    <div class="title">
      <b-navbar
        class="rounded-top"
        toggleable="lg"
        type="light"
        variant="secondary"
      >
        <b-navbar-brand class="ml-2">
          <img src="../assets/logo.png" class="logo" alt="" />
          <b>{{ appName }}</b>
        </b-navbar-brand>
      </b-navbar>
    </div>

    <b-card class="p-0 h-99 rounded-bottom">
      <b-container class="m-0 p-0">
        <b-row no-gutters>
          <b-col cols="5">
            <BestTransportForm @formSubmit="submitFormHandler" />
          </b-col>
          <b-col cols="6"> This is another Component </b-col>
        </b-row>
      </b-container>
    </b-card>
  </section>
</template>

<script>
import { BNavbar, BNavbarBrand, BCard } from "bootstrap-vue";

import BestTransportForm from "./BestTransportForm";

export default {
  components: {
    BNavbar,
    BNavbarBrand,
    BCard,
    BestTransportForm
  },
  data() {
    const appName = "";

    return {
      appName
    };
  },
  created() {
    // Implemente aqui o GET dos dados da API REST
    // para que isso ocorra na inicialização da pagina
    this.appName = "Melhor Frete";
  },
  methods: {
    // Implemente aqui os metodos utilizados na pagina
    methodFoo() {
      console.log(this.appName);
    },
    submitFormHandler(evt) {
      console.log(evt.peso, evt.estado);
    }
  }
};
</script>

<style scoped>
.title .navbar-brand {
  margin-left: 20px;
  font-weight: 600;
}

.analise-section {
  height: 90vh;
}

.logo {
  width: 28px;
  margin-right: 10px;
}
</style>
