<template>
  <b-container class="p-0 mb-2">
    <b-row>
      <b-col cols="8">
        <b-card no-body class="overflow-hidden">
          <b-row no-gutters>
            <b-col
              cols="3"
              class="bg-secondary d-flex justify-content-center align-items-center"
            >
              <img :src="require('@/assets/icons/' + this.iconSrc)" alt="" />
            </b-col>
            <b-col
              cols="9"
              class="px-2 py-3"
              :class="{ 'bg-light': this.isDarker }"
            >
              <h3 class="h5">{{ this.cardTitle }}</h3>
              <p class="mb-0">Transportadora: {{ this.cota.name }}</p>
              <p>Tempo Estimado: {{ this.cota.lead_time }}</p>
            </b-col>
          </b-row>
        </b-card>
      </b-col>
      <b-col cols="4" class="h-20 p-0">
        <b-card
          title="Preço"
          class="h-100"
          :class="{ 'bg-light': this.isDarker }"
        >
          <b-card-body class="p-0">
            <p>R$ {{ this.preco.toFixed(2) }}</p>
          </b-card-body>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import { BCard, BCardBody, BContainer, BRow, BCol } from "bootstrap-vue";

export default {
  props: {
    isDarker: Boolean,
    iconSrc: String,
    cota: Object,
    cardTitle: String,
    preco: Number
  },
  components: {
    BCard,
    BCardBody,
    BContainer,
    BRow,
    BCol
  }
};
</script>

<style>
.icon {
  width: 48px;
  height: 48px;
}
</style>
