<template>
  <b-form class="p-4 bg-light h-100" @submit="submitHandler">
    <h3 class="h5 mb-5 heading-tertiary">
      <img
        src="../assets/icons/timezone-48.png"
        class="icon-map"
        alt="Map icon"
      />
      Insira o destino e o peso
    </h3>

    <b-form-group id="destino-group" class="mb-3">
      <label for="destino" class="font-weight-bolder">Destino</label>
      <b-form-select
        id="destino"
        required
        v-model="cidadeSelected"
        :options="cidades"
      />
    </b-form-group>

    <b-form-group id="peso-group" class="mb-5">
      <label for="destino" class="font-weight-bolder">Peso</label>
      <b-form-input
        v-model="peso"
        id="peso"
        type="text"
        placeholder="Insira o peso em KG"
        required
      />
    </b-form-group>

    <b-form-group class="text-center">
      <b-button class="btn" variant="secondary" type="submit"
        >Analisar</b-button
      >
    </b-form-group>
  </b-form>
</template>

<script>
import {
  BForm,
  BFormGroup,
  BFormSelect,
  BFormInput,
  BButton
} from "bootstrap-vue";

export default {
  components: {
    BForm,
    BFormGroup,
    BFormSelect,
    BFormInput,
    BButton
  },

  emits: ["form-submit"],

  data() {
    return {
      peso: 0,
      cidadeSelected: null,
      cidades: [
        { text: "Selecione o Destino", value: null },
        "Belo Horizonte",
        "Campinas",
        "Curitiba",
        "Fortaleza",
        "Manaus",
        "Natal",
        "Recife",
        "Rio de Janeiro",
        "Salvador",
        "São Paulo"
      ]
    };
  },
  methods: {
    submitHandler(evt) {
      evt.preventDefault();
      this.$emit("formSubmit", {
        peso: this.peso,
        cidade: this.cidadeSelected
      });
    }
  }
};
</script>

<style lang="scss">
.map-icon {
  width: 28px;
}
</style>
