<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  tarefaTemporaria: '',
  filtro: 'todas',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false
    },
    {
      titulo: 'Estudar React',
      finalizada: false
    },
    {
      titulo: 'Estudar JS',
      finalizada: true
    },
  ]
})

const tarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const tarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const tarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return tarefasPendentes();

    case 'finalizadas':
      return tarefasFinalizadas();

    default:
      return estado.tarefas;

  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false
  }

  estado.tarefas.push(tarefaNova);
  estado.tarefaTemporaria = '';
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="tarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemporaria"
      :edita-tarefa-temp="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="tarefasFiltradas()" :filtro-atual="estado.filtro" />
  </div>
</template>

