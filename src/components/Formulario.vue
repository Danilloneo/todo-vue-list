<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>
<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row d-flex">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div><!--col-->
            <div class="col-md-2 ms-4">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div><!--col-md-2-->
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                <option value="todas">Todas tarefas</option>
                <option value="pendentes">Pedentes</option>
                <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div><!--row-->
    </form>
</template>