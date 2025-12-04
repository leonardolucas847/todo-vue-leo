<script setup>
  import {reactive} from 'vue'
  const estado = reactive({
    filtro: 'todas', 
    tarefas: [
      {
      titulo:"Estudar curso EBAC",
      finalizada: false,
      },{
      titulo:"Estudar aulas-Pedro",
      finalizada: false,
      },{
      titulo:"Estudar curso EBAC",
      finalizada: true,
      },
  ],
  tarefaAInserir: '',
});
function cadastraTarefa(){
  estado.tarefas.push({titulo: estado.tarefaAInserir,
    finalizada: false,
  })
  estado.tarefaAInserir= '';
};
const  getTarefapendente = () => {
  return estado.tarefas.filter(tarefa=> tarefa.finalizada === false)
}
const  getTarefaFinalizadas = () => {
  return estado.tarefas.filter(tarefa=> tarefa.finalizada === true)
}

const getTarefasFiltradas = () => {
    const filtro = estado.filtro;
    switch (filtro) {
      case 'pendentes':
        return getTarefapendente();
      case 'finalizadas':
        return getTarefaFinalizadas();
      default:
        return estado.tarefas;
    }
}
</script>


<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{getTarefapendente().length}} tarefas pendetes.
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input  @keyup="evento => estado.tarefaAInserir = evento.target.value" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select  @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
        </div>
    </form>
    <ul class="list-group mt-4">
        <li  class="list-group-item" v-for="tarefa in getTarefasFiltradas()" >
          <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
          <label class="ms-3" :for="tarefa.titulo">
            {{ tarefa.titulo }}
          </label>
        </li>
    </ul>
  </div>
</template>

<style scoped></style>
