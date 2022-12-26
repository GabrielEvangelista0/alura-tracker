<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoAlterarModoEscuro="trocarTema"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioVue @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <TarefaVue v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <BoxVue v-if="listaEstaVazia">
          Você não esta muito produtivo hoje :(
        </BoxVue>
      </div>

    </div>
  </main>
</template>

<script lang="ts">
import { compile, defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import BoxVue from './components/Box.vue';
import FormularioVue from './components/Formulario.vue';
import TarefaVue from './components/Tarefa.vue';
import ITarefa from './interfaces/ITarefa';

export default defineComponent({

  name: 'App',
  components: {
    BarraLateral,
    FormularioVue,
    TarefaVue,
    BoxVue
  },

  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false
    }
  },

  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
    },

    trocarTema(modoEscuroAtivo: boolean){
      this.modoEscuroAtivo = modoEscuroAtivo


    }
  },

  computed:{
    listaEstaVazia() : boolean {
      return this.tarefas.length === 0
    }
  }


});
</script>


<style>
.lista {
  padding: 1.25rem;
}

main{
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}

.conteudo{
  background-color: var(--bg-primario);
}
</style>
