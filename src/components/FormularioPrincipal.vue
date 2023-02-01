<template>
    <div class="box formulario">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulario para criação de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao">
            </div>
            <div class="column">
                <TemporizadorPrincipal @aoTemporizadorFinalizado="finalizarTarefa"/>
            </div>
        </div>
    </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue'
import TemporizadorPrincipal from './TemporizadorPrincipal.vue'

export default defineComponent({
    name: "FormularioPrincipal",
    emits: ['aoSalvarTarefa'],
    components: {
        TemporizadorPrincipal
    },
    data() {
        return {
            descricao: ''
        }
    },
    methods: {
        finalizarTarefa(tempoDecorrido: number): void {
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao
            })
            console.log('Tempo da tarefa: ', tempoDecorrido)
            console.log('Descrição da tarefa: ', this.descricao)
            this.descricao = ''
        }
    }
})

</script>

<style>
.formulario {
    background-color: var(--bg-primario);
    color: var(--texto-primario);
}
</style>