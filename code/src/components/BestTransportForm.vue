<template>
  <b-form class="p-4 bg-light h-100" @submit="submitHandler">
    <h3 class="h5 mb-5 heading-tertiary">
      <img src="../assets/icons/map-48.png" class="icon-map" alt="Map icon" />
      Insira o destino e o peso
    </h3>

    <b-form-group
      id="destino-group"
      label="Destino:"
      label-for="destino"
      class="mb-3"
    >
      <b-form-select
        id="destino"
        required
        v-model="estadoSelected"
        :options="estados"
      />
    </b-form-group>

    <b-form-group id="peso-group" label="Peso:" label-for="peso" class="mb-5">
      <b-form-input v-model="peso" id="peso" required />
    </b-form-group>

    <b-form-group class="text-center">
      <b-button class="btn px-5" variant="secondary" type="submit"
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
      estadoSelected: null,
      estados: [
        { text: "Selecione o Destino", value: null },
        "Campinas",
        "São Paulo",
        "Limeira"
      ]
    };
  },
  methods: {
    submitHandler(evt) {
      evt.preventDefault();
      this.$emit("formSubmit", {
        peso: this.peso,
        estado: this.estadoSelected
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
