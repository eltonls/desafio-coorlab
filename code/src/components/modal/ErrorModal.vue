<template>
  <b-modal id="modal-1" centered hide-header hide-footer>
    <template default="{ close }">
      <div class="px-8 py-4 text-center">
        <img
          src="../../assets/icons/danger-48.png"
          alt="Exclamation mark, danger icon"
          class="mb-4"
        />
        <h5 class="font-weight-normal mb-4">
          Insira os valores para realizar a análise
        </h5>

        <b-button variant="secondary" @click="this.closeModal">Fechar</b-button>
      </div>
    </template>
  </b-modal>
</template>

<script>
import { BModal, BButton } from "bootstrap-vue";
export default {
  components: {
    BModal,
    BButton
  },
  methods: {
    closeModal() {
      this.$bvModal.hide("modal-1");
    }
  }
};
</script>

<style></style>
