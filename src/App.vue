<script setup>
  import { ref } from 'vue'
  let tarefas = ref([
    { id: 1, desc: 'Tarefa 1', status: 'pendente' },
    { id: 2, desc: 'Tarefa 2', status: 'concluida' }
  ])
  const novaTarefa = ref('')
  const posicaoAlterar = ref(-1)
  function addTarefa() {
    if (posicaoAlterar.value == -1) {
    let maiorID = Math.max(...tarefas.value.map(item => item.id))
    tarefas.value.push({ id: maiorID + 1, desc: novaTarefa.value, status: 'pendente' });
    novaTarefa.value = '';
  }
  else {
    tarefas.value[posicaoAlterar.value].desc = novaTarefa.value;
    posicaoAlterar.value = -1;
    novaTarefa.value = ''
  }
}
  
  function deleteTarefa(item) {
    const posicao = tarefas.value.findIndex(t => t.id === item.id);
    tarefas.value.splice(posicao, 1)
  }

  function editarTarefa(item) {
    posicaoAlterar.value = tarefas.value.findIndex(t => t.id === item.id);
    novaTarefa.value = tarefas.value[posicaoAlterar.value].desc;
  }
</script>

<template>
  <div class="container">
    <input type="text" v-model="novaTarefa">
    <button @click="addTarefa">Adicionar</button>
    <ul>
      <li v-for="item in tarefas" :key="item.id">
        {{ item.desc }}
        <span>
          <a href="#" @click.prevent="deleteTarefa(item)">Delete</a>
          <a href="#" @click.prevent="editarTarefa(item)">Edit</a>
        </span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
</style>
