<template>
  <header>
    <h1>
      <img src="../assets/logo.png" alt="alura tracker">
    </h1>
    <button class="button" @click="ativarModoEscuro">
      {{ textoDoBotao }}
    </button>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: "BarraLateral",

  emits: ["aoAlterarModoEscuro"],

  data() {
      return {
        modoEscuroAtivo: false,
      }
  },

  computed: {
    textoDoBotao(){
      if(this.modoEscuroAtivo){
        return 'Desativar modo escuro'
      }else{
        return 'Ativar modo escuro'
      }
    }
  },

  methods: {
    ativarModoEscuro(){
      this.modoEscuroAtivo = !this.modoEscuroAtivo
      this.$emit('aoAlterarModoEscuro', this.modoEscuroAtivo)
    }

  }

})
</script>

<style scoped>
header {
  padding: 1rem;
  background: #0d3b66;
  width: 100%;
  height: 100vh;
  text-align: center;
}

@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>