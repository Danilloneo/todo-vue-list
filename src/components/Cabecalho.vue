<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p v-if="tarefasPendentes > 0">
            Você possuí {{ props.tarefasPendentes }} tarefas pendentes
        </p>
        <span v-else>Você não possuí tarefas pendentes</span>
    </header>
</template>

<!--f1 transform document o vs code indenta-->
<!--propriedades nada mais é do que um atributo com o src etc
Quando agente quer passar informações para outra arquivo damos os nome propriedade-->