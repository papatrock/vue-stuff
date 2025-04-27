<script>
import Tag from './Tag.vue';

export default{
    components: {Tag},

    props:{
        ingrediente: {type: String, required:true}
    },
    data() {
        return {
            selecionado: false
        }
    },
    methods: {
        aoClicar() {
           this.selecionado = !this.selecionado;

           if(this.selecionado){
                        // nome do evento,  data
                this.$emit('adicionarIngrediente',this.ingrediente);
           }
           else {
                this.$emit('removerIngrediente',this.ingrediente);
           }
        }
    },
    emits:['adicionarIngrediente']

}
</script>

<template>                      <!-- @click tbm funciona-->
    <button class="ingrediente" v-on:click="aoClicar()">
        <Tag :texto="ingrediente" :ativa="selecionado"/>
    </button>
</template>

<style scoped>

.ingrediente{
    cursor: pointer;
}
</style>