<script setup>
import { reactive } from 'vue';


const estado = reactive({
  filtro: 'operacao',
  NumeroTemp: '',
  operacao: [
    {
      valor: true,
    },
  ]
})

const getOperacaoSomar = () => {
  return estado.tarefas.filtro(tarefa => tarefa.somar)
}

const getOperacaoDiminuir = () => {
  return estado.tarefas.filtro(tarefa => tarefa.diminuir)
}

const getOperacaoMultiplicacao = () => {
  return estado.tarefas.filtro(tarefa => tarefa.multiplicacao)
}

const getOperacaoDivisao = () => {
  return estado.tarefas.filtro(tarefa => tarefa.divisao)
}

const getOperacaoFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'somar':
      return getOperacaoSomar();
    case 'diminuir':
      return getOperacaoDiminuir();
    case 'multiplicacao':
      return getOperacaoMultiplicacao();
    case 'divisao':
      return getOperacaoDivisao();
    default:
      return estado.tarefas;
  }
}

const cadastraNumero01 = () => {
  const numeroNovo = {
    valor: estado.NumeroTemp,
  }
  estado.tarefas.push(numeroNovo);
}

const cadastraNumero02 = () => {
  const numeroNovo = {
    valor: estado.NumeroTemp,
  }
  estado.tarefas.push(numeroNovo);
}


</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-primary rounded-3">
      <h1>Calculadora Aritmética</h1>
    </header>

    <div class="row">
      <div class="col-md-2">
        <input required @change="evento => estado.NumeroTemp = evento.target.value" @submit="cadastraNumero01" type="number"
          placeholder="Nº">
      </div>
      <div class="col-md-2">
        <select class="ms-4" @change="evento => estado.filtro = evento.target.value">
          <option value="operações">Operações</option>
          <option value="somar">+</option>
          <option value="diminuir">-</option>
          <option value="multiplicacao">*</option>
          <option value="divisao">/</option>
        </select>
      </div>
      <div class="col-md-2">
        <input required @change="evento => estado.NumeroTemp = evento.target.value" @submit="cadastraNumero02" type="number"
          placeholder="Nº">
      </div>
      <div class="col-md-1">
        <span class="ms-3">=</span>
      </div>
      <div class="col-md-2">
        <input type="text" placeholder="R">
      </div>
    </div>
  </div>
</template>

<style scoped>

h1 {
  text-align: center;
}

.row {
  align-items: center;
  text-align: center;
  justify-content: center;
}

input {
  border-color: blue;
  border-radius: 3px;
}

select {
  border-radius: 3px;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  background-color: rgba(94, 94, 243, 0.562);
}

</style>
