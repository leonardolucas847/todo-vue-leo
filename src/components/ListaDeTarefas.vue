<script setup>
    const props = defineProps(['tarefas', 'mostraLista'])
</script>

<template>
    <ul v-if="props.mostraLista"  class=" list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento=> tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
            <label class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <span v-else >Você nao possui tarefas cadastradas </span>
</template>
