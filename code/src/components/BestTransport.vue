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
          <b-col cols="4">
            <BestTransportForm @formSubmit="submitFormHandler" />
          </b-col>
          <b-col cols="8" class="px-2 py-5">
            <h3 class="h5 font-weight-normal">
              Estas são as melhores alternativas de frete que encontramos para
              você
            </h3>
            <BestTransportCard
              :isDarker="true"
              :cota="this.cotaDeMenorPreco"
              iconSrc="receive-cash-64.png"
              cardTitle="Frete com menor valor"
              :preco="this.precoCotaEconomica"
            />
            <BestTransportCard
              :isDarker="false"
              :cota="this.cotaMaisRapida"
              iconSrc="clock-48.png"
              cardTitle="Frete mais rápido"
              :preco="this.PrecoCotaRapida"
            />
          </b-col>
        </b-row>
      </b-container>
    </b-card>
  </section>
</template>

<script>
import { BNavbar, BNavbarBrand, BCard } from "bootstrap-vue";

import BestTransportForm from "./BestTransportForm";
import BestTransportCard from "./BestTransportCard";

export default {
  components: {
    BNavbar,
    BNavbarBrand,
    BCard,
    BestTransportForm,
    BestTransportCard
  },
  data() {
    const appName = "";

    return {
      appName,
      cotacoes: null,
      cotaDeMenorPreco: {},
      cotaMaisRapida: {},
      precoCotaEconomica: 0,
      PrecoCotaRapida: 0
    };
  },
  async created() {
    // Implemente aqui o GET dos dados da API REST
    // para que isso ocorra na inicialização da pagina
    this.appName = "Melhor Frete";

    const res = await fetch("http://localhost:3000/transport");
    let data = await res.json();
    this.cotacoes = data;
  },
  methods: {
    // Implemente aqui os metodos utilizados na pagina
    submitFormHandler(evt) {
      const cotacoesDaCidade = this.cotacoes.filter(cota => {
        return cota.city.toLowerCase() === evt.cidade.toLowerCase();
      });

      this.getFreteEconomico(evt.peso, cotacoesDaCidade);
      this.getFreteMaisRapido(evt.peso, cotacoesDaCidade);
    },
    getMenorFreteLeve(cotacoes) {
      let cotaMenorPreco = cotacoes[0];
      cotacoes.forEach(cota => {
        if (cotaMenorPreco.cost_transport_light > cota.cost_transport_light) {
          cotaMenorPreco = cota;
        }
      });

      return cotaMenorPreco;
    },
    getMenorFretePesado(cotacoes) {
      let cotaMenorPreco = cotacoes[0];
      cotacoes.forEach(cota => {
        if (cotaMenorPreco.cost_transport_heavy > cota.cost_transport_heavy) {
          cotaMenorPreco = cota;
        }
      });

      return cotaMenorPreco;
    },
    getPrecoFrete(peso, custo) {
      return peso * Number(custo);
    },
    getFreteEconomico(peso, cotacoes) {
      if (peso > 100) {
        this.cotaDeMenorPreco = this.getMenorFretePesado(cotacoes);
        const custo = this.cotaDeMenorPreco.cost_transport_heavy.slice(2);
        this.precoCotaEconomica = this.getPrecoFrete(peso, custo);
      } else {
        this.cotaDeMenorPreco = this.getMenorFreteLeve(cotacoes);
        const custo = this.cotaDeMenorPreco.cost_transport_light.slice(2);
        this.precoCotaEconomica = this.getPrecoFrete(peso, custo);
      }
    },
    getFreteMaisRapido(peso, cotacoes) {
      let freteMaisRapido = cotacoes[0];
      cotacoes.forEach(cota => {
        const novoTempoEstimado = cota.lead_time.replace(/\D/g, "");
        const atualTempoEstimado = freteMaisRapido.lead_time.replace(/\D/g, "");

        console.log("Novo Tempo:", novoTempoEstimado);
        console.log("Atual Tempo:", atualTempoEstimado);

        if (Number(novoTempoEstimado) < Number(atualTempoEstimado)) {
          freteMaisRapido = cota;
        }
      });

      this.cotaMaisRapida = freteMaisRapido;

      if (peso > 100) {
        const custoPesado = this.cotaMaisRapida.cost_transport_heavy.slice(2);

        this.PrecoCotaRapida = this.getPrecoFrete(peso, custoPesado);
      } else {
        const custoLeve = this.cotaMaisRapida.cost_transport_light.slice(2);

        this.PrecoCotaRapida = this.getPrecoFrete(peso, custoLeve);
      }
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
