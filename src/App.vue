<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';
const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefa: [
    // {
    //   titulo: 'AAAA',
    //   finalizado: false,
    // },
    // {
    //   titulo: 'BBBBB',
    //   finalizado: false,
    // },
    // {
    //   titulo: 'CCCC',
    //   finalizado: true,
    // }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefa.filter(tarefa => !tarefa.finalizado)
}

const getTarefasFinalizadas = () => {
  return estado.tarefa.filter(tarefa => tarefa.finalizado)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();

    case 'finalizadas':
      return getTarefasFinalizadas();

    default:
      return estado.tarefa;
  }
}

const cadastrarTarefa = () => {
  // e.preventDefault()
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizado: false,
  }
  estado.tarefa.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastrarTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div><!--container-->
</template>

<style scoped>
* {
  list-style-type: none;
}
</style>