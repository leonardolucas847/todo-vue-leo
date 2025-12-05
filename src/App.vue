<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


const estado = reactive({
  mostraLista: false,
  filtro: 'todas',
  tarefas: [
    {
      titulo: "Estudar curso EBAC",
      finalizada: false,
    }, {
      titulo: "Estudar aulas-Pedro",
      finalizada: false,
    }, {
      titulo: "Estudar Inglês",
      finalizada: true,
    },
],
  tarefaAInserir: '',
});
function cadastraTarefa() {
  estado.tarefas.push({
    titulo: estado.tarefaAInserir,
    finalizada: false,
  })
  estado.tarefaAInserir = '';

};
const getTarefapendente = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
}
const getTarefaFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
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
const mostraListaDeTarefas = () => {
  return estado.tarefas.length > 0
}
</script>


<template>
  <div class="container">
    <cabecalho :tarefasPendentes="getTarefapendente().length" />
    <Formulario :trocaFiltro="evento => estado.filtro = evento.target.value" :tarefaAInserir="estado.tarefaAInserir" :editaTarefaInserida="evento => estado.tarefaAInserir = evento.target.value" :cadastraTarefa="cadastraTarefa" /> 
    <ListaDeTarefas :mostraLista="mostraListaDeTarefas()" :tarefas="getTarefasFiltradas()" />
  </div>
</template>

<style scoped></style>
