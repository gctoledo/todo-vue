<script setup>
const props = defineProps(['tarefas', 'filtroAtual'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas" v-if="tarefas.length > 0">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
        <span v-else>Você não possui tarefas {{ props.filtroAtual }}!</span>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>