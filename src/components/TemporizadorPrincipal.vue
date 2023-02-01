<template>
    <section class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroPrincipal :tempoEmSegundos="tempoEmSegundos" />
        <BotaoComponent @clicado="iniciaContagem" icone="fas fa-play" texto="play" :desabilitado="cronometroRodando" />
        <BotaoComponent @clicado="finalizaContagem" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroRodando" />
    </section>
</template>
  

<script lang="ts">

import { defineComponent } from 'vue'
import CronometroPrincipal from './CronometroPrincipal.vue'
import BotaoComponent from './BotaoComponent.vue'

export default defineComponent({
    name: "TemporizadorPrincipal",
    emits: ['aoTemporizadorFinalizado'],
    components: {
        CronometroPrincipal,
        BotaoComponent
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: {
        iniciaContagem() {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 1000)
            console.log('Inicializando contagem...')
        },
        finalizaContagem() {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})

</script>