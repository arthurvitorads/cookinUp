<template>
    <main class="conteudo-principal">
      <SuaLista :ingredientes="ingredientes" />
      <SelectIngredientes v-if="conteudo === 'SelecionarIngredientes'"
      @adicionar-ingrediente="adicionarIngredientes"
      @remover-ingrediente="removerIngredientes" 
      @buscarReceitas="conteudo = 'MostrarReceitas'"/>
      <MostrarReceitas v-else-if="conteudo === 'MostrarReceitas'"/>
    </main>
</template>

<style scoped>
.conteudo-principal {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #FFFAF3);
  color: var(--cinza, #444);

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

@media only screen and (max-width: 1300px) {
  .conteudo-principal {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .conteudo-principal {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>

<script lang="ts">
import SelectIngredientes from './SelectIngredientes.vue'
import SuaLista from './SuaLista.vue'
import Tag from './Tag.vue'
import MostrarReceitas from './MostrarReceitas.vue'

type Pagina = 'SelecionarIngredientes' | 'MostrarReceitas'

    export default{
        components: {
            SuaLista: SuaLista,
            SelectIngredientes: SelectIngredientes,
            Tag: Tag,
            MostrarReceitas: MostrarReceitas
        },
        data(){
            return{
                ingredientes: [],
                conteudo: 'SelecionarIngredientes' as Pagina
            }
        },
        methods: {
          adicionarIngredientes(ingrediente: string) {
            if (!this.ingredientes.includes(ingrediente)) {
              this.ingredientes.push(ingrediente);
            }
          },
          removerIngredientes(ingrediente: string) {
            this.ingredientes = this.ingredientes.filter(item => item !== ingrediente);
          },
          navegar(pagina: Pagina){
            this.conteudo = 'MostrarReceitas'
          }
        }
    }
</script>