<template>
    <section>
        <span class="subtitulo-lg sua-lista-texto">
            Sua lista:
        </span>
        <ul v-if="ingredientes.length > 0" class = "ingredientes-sua-lista">
            <li v-for = "ingrediente in ingredientes" :key="ingrediente">
            <Tag :texto="ingrediente" :class="{active: true}"/>
            </li>
        </ul>
        <p v-else="ingredientes.length == 0" class="paragrafo lista-vazia">
            <img src="../assets/images/icones/lista-vazia.svg" alt="">
            Sua lista esta vazia, selecione os ingredientes para comecar!
        </p>
    </section>  
</template>

<script lang="ts">
    import Tag from "@/components/Tag.vue";
    import type { PropType } from 'vue';

    export default {
        components: { Tag },
        props: {
        ingredientes: { type: Array as PropType<string[]>, required: true }
        },
    }
</script>


<style scoped>
.sua-lista-texto {
  color: var(--coral, #F0633C);
  display: block;
  text-align: center;
  margin-bottom: 1.5rem;
}

.ingredientes-sua-lista {
  display: flex;
  justify-content: center;
  gap: 1rem 1.5rem;
  flex-wrap: wrap;
}

.lista-vazia {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.25rem;

  color: var(--coral, #F0633C);
  text-align: center;
}
</style>