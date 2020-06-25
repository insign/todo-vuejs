<template>
  <div id="app">
    <h1>Lista de tarefas</h1>

    <input type="text" @keydown.enter="adicionar" v-model="nova.tarefa">
    <button @click="adicionar">Adicionar</button>

    <ul v-for="tarefa in por_fazer" :key="tarefa.tarefa">
      <input type="checkbox" v-model="tarefa.feito" :checked="tarefa.feito">
      <li :class="tarefa.feito ? 'feita' : ''">{{tarefa.tarefa}}</li>
    </ul>
    <ul v-for="tarefa in feitas" :key="tarefa.tarefa">
      <input type="checkbox" v-model="tarefa.feito" :checked="tarefa.feito">
      <li :class="tarefa.feito ? 'feita' : ''">{{tarefa.tarefa}}</li>&nbsp;
      <button type="button" @click="tarefa.arquivado=true">arquivar</button>
    </ul>
  </div>
</template>

<script>

export default {
  name: "todo",
  mouted() {

  },
  created() {

  },
  data: function() {
    return {
      tarefas: [],
      nova: { tarefa: "", feito: false, arquivado: false }
    };
  },
  methods: {
    adicionar() {
      this.tarefas.push(this.nova);
      this.resetar();
    },
    resetar() {
      this.nova = { tarefa: "", feito: false, arquivado: false };
    }
  },
  computed: {
    todas() {
      return this.tarefas.filter(x => !x.arquivado);
    },
    por_fazer() {
      return this.todas.filter(x => !x.feito);
    },
    feitas() {
      return this.todas.filter(x => x.feito);
    }
  }
};
</script>

<style>
ul {
  padding-left: 0;
}

li {
  list-style-type: none;
  display: inline;
  font-size: 1.4rem;
  padding-left: 10px;
}

.feita {
  text-decoration: line-through;
  color: grey;
}

input[type="checkbox"] {
  transform: scale(2);
  margin: 10px;
}
</style>
