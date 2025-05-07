<template>
  <main
    :class="{ 'modo-escuro': modoEscuroAtivo }"
    class="columns is-gapless is-multiline"
  >
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioTarefa @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <Tarefa
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
        <Box v-if="listaEstaVazia">
          Você não está muito produtivo hoje! &#128553; &#128549;</Box
        >
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import FormularioTarefa from "./components/FormularioTarefa.vue";
import Tarefa from "./components/Tarefa.vue";
import ITarefa from "./interfaces/ITarefa";
import Box from "./components/Box.vue";
export default defineComponent({
  name: "App",
  components: {
    BarraLateral,
    FormularioTarefa,
    Tarefa,
    Box,
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
    };
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
  },
});
</script>

<style>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2d2d42;
  --texto-primario: #ddd;
}

main.modo-escuro .box {
  box-shadow: 0 4px 6px rgba(255, 255, 255, 0.1); /* Sombra mais clara no modo escuro */
}

.conteudo {
  background: var(--bg-primario);
}
</style>
