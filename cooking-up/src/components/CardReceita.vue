<script>

    export default{
        props:{
            receita: {type: Object, required: true},
        }
    }
</script>

<template>
    <img :src="`/imagens/receitas/${receita.imagem}`" alt="" class="receita_imagem">
    <h2>{{ receita.nome }}</h2>

</template>