<template>
  <header>
    <h1>
      <img src="../assets/logo.png" alt="Logo Alura Tracker" />
    </h1>
    <Botao
      :icone="modoEscuroAtivo ? 'fas fa-cloud-sun' : 'fas fa-cloud-moon'"
      :texto="modoEscuroAtivo ? 'Ativar modo claro' : 'Ativar modo escuro'"
      @clicado="alterarTema"
    />
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Botao from "./Botao.vue";

export default defineComponent({
  name: "BarraLateral",
  components: {
    Botao,
  },
  emits: ['aoTemaAlterado'],
  data () {
    return {
      modoEscuroAtivo: false
    }
  },
  methods: {
    alterarTema () {
      this.modoEscuroAtivo = !this.modoEscuroAtivo
      this.$emit('aoTemaAlterado', this.modoEscuroAtivo)
    }
  }
});
</script>

<style scoped>
header {
  padding: 1rem;
  background: #0d3b66;
  width: 100%;
  height: 100vh;
}
@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>
