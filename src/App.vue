<script setup>
  import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefa: [
      // {
      //   titulo: '',
      //   finalizado: false,
      // },
      // {
      //   titulo: '',
      //   finalizado: false,
      // },
      // {
      //   titulo: '',
      //   finalizado: false,
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
    estado.tarefaTemp= '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possuí {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="rou d-flex">
          <div class="col">
            <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
          </div><!--col-->
          <div class="col-md-2 ms-4">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
          </div><!--col-md-2-->
          <div class="col-md-2">
            <select @change="evento => estado.filtro = evento.target.value" class="form-control">
              <option value="todas">Todas tarefas</option>
              <option value="pendentes">Pedentes</option>
              <option value="finalizadas">Finalizadas</option>
            </select>
          </div>
      </div><!--row-->
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizado }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div><!--container-->
</template>

<style scoped>
  * {
    list-style-type: none;
  }

  .done {
    text-decoration: line-through;
  }
</style>

