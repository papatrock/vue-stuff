<script>
import { obterReceitas } from '@/http';
import BotaoPrincipal from './BotaoPrincipal.vue';
import CardReceita from './CardReceita.vue';
import { itensDeLista1EstaoEmLista2 } from '@/operacoes/listas';

    export default {
        props:{
            ingredientes: { type: Array, required: true}
        },
        data() {
            return {
                receitas: []
            }
        },
        components: {
            BotaoPrincipal, CardReceita
        },
        emits:['troca-navegar'],

        async created(){
            const receitas = await obterReceitas();

            this.receitas = receitas.filter((receita) => {
                //todos os ingredientes de uma receita devem estar inclusos na minha lista de ingredientes
                const possoFazerReceita = itensDeLista1EstaoEmLista2(receita.ingredientes, this.ingredientes);

                return possoFazerReceita;
            })
        }
    }
</script>

<template>

    <ul class="receitas">
        <h1>Resultados encontrados: {{ receitas.length }}</h1>
        <li v-for="receita in receitas" :key="receita.nome">
           <CardReceita :receita="receita"/>

        </li>
    </ul>
    <BotaoPrincipal :texto="'Editar Lista'"
    @click="$emit('troca-navegar')"/>
</template>