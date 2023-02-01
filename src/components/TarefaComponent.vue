<template>
    <BoxComponent>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem Descrição' }}
            </div>
            <div class="column">
                <CronometroPrincipal :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
            </div>
        </div>
    </BoxComponent>
</template>

<script lang="ts">

import { defineComponent, PropType } from 'vue';
import BoxComponent from './BoxComponent.vue';
import CronometroPrincipal from './CronometroPrincipal.vue';
import ITarefa from '@/interfaces/ITarefa';

export default defineComponent({
    name: 'TarefaComponent',
    components: {
        CronometroPrincipal,
        BoxComponent
    },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
})

</script>