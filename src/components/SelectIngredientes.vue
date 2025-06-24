<script lang="ts">
import { obterCategorias } from '@/http';
import CardCategoria from './CardCategoria.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';
    export default {
        components: {
            CardCategoria: CardCategoria,
            BotaoPrincipal: BotaoPrincipal
        },
        data(){
            return{
                categorias: []
            }
        },
        async created() {
            this.categorias = await obterCategorias ()
        },
        emits: ['adicionarIngrediente', 'removerIngrediente', 'buscarReceitas']
    }
</script>

<template>
    <section class="selecionar-ingredientes">
        <h1 class="cabecalho titulo-ingredientes">Ingredientes</h1>

        <p class="paragrafo-lg instrucoes">
            Selecione os ingredientes: 
        </p>

        <ul class="categorias">
            <li v-for="categoria in categorias" :key="categoria.nome">
                <CardCategoria :categoria="categoria"
                @adicionar-ingrediente="$emit('adicionarIngrediente', $event)"
                @remover-ingrediente="$emit('removerIngrediente', $event)" />
            </li>
        </ul>

        <p class="paragrafo dica">
            ATENCAO: Consideramos que voce tenha sal, pimenta e agua em casa!
        </p>

        <BotaoPrincipal texto="Buscar receitas!" @click="$emit('buscarReceitas')"/>
    </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}
</style>