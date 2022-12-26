<template>
    <div class="column">
        <div class="is-flex is-align-items-center is-justify-content-space-between">
            <CronometroVue :tempoEmSegundos="tempoEmSegundos" />
            <button class="button" @click="iniciar" :disabled="cronometroEstaRodando">
                <span class="icon">
                    <i class="fas fa-play"></i>
                </span>
                <span>play</span>
            </button>
            <button class="button" @click="finalizar" :disabled="!cronometroEstaRodando">
                <span class="icon">
                    <i class="fas fa-stop"></i>
                </span>
                <span>stop</span>
            </button>
        </div>
    </div>
</template>


<script lang="ts">

import { defineComponent } from 'vue'
import CronometroVue from './Cronometro.vue'

export default defineComponent({
    name: 'TemporizadorVue',
    components: {
      CronometroVue
    },
    emits: ['aoTemporizadorFinalizado'],

    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroEstaRodando: false
        }
    },


    methods: {
        iniciar() {
            this.cronometroEstaRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos++
            }, 1000)
        },

        finalizar(){
            this.cronometroEstaRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})

</script>