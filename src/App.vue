<script setup>
import { reactive } from 'vue';


const estado = reactive({
  filtro: 'operacao',
  NumeroTemp1: '',
  NumeroTemp2: '',
  operacao: [
    {
      valor: true,
    },
  ]
})

const somar = (num1, num2) => {
  return num1 + num2;
}

const subtrair = (num1, num2) => {
  return num1 - num2;
}

const multiplicar = (num1, num2) => {
  return num1 * num2;
}

const dividir = (num1, num2) => {
  if (num2 !== 0) {
    return num1 / num2;
  } else {
    return "Divisão por zero não é permitido";
  }
}

const calcularResultado = () => {
  const num1 = parseFloat(estado.NumeroTemp1);
  const num2 = parseFloat(estado.NumeroTemp2);
  let resultado = 0;

  switch (estado.filtro) {
    case 'somar':
      resultado = somar(num1, num2);
      break;
    case 'diminuir':
      resultado = subtrair(num1, num2);
      break;
    case 'multiplicacao':
      resultado = multiplicar(num1, num2);
      break;
    case 'divisao':
      resultado = dividir(num1, num2);
      break;
    default:
      break;
  }

  estado.resultado = resultado;
}

const cadastraNumero01 = () => {
  const numeroNovo = {
    valor: estado.NumeroTemp1,
}
  estado.tarefas.push(numeroNovo);
}

const cadastraNumero02 = () => {
  const numeroNovo = {
    valor: estado.NumeroTemp2,
}
  estado.tarefas.push(numeroNovo);
}


</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-primary rounded-3">
      <h1>Calculadora Aritmética</h1>
    </header>

    <div>
      <h2 class="sub">INSTRUÇÕES</h2>
      <h4 class="text">Primeiro, insira os números nos campos correspondentes</h4>
      <h4 class="text">Em seguida, escolha a operação desejada</h4>
    </div>
    <div class="row bg-success rounded-3 p-5">
      <div class="col-md-2">
        <input required @change="evento => estado.NumeroTemp1 = evento.target.value" @submit="cadastraNumero01" type="number"
          placeholder="Nº">
      </div>
        <div class="col-md-2">
          <select v-model="estado.filtro" class="ms-4" @change="calcularResultado">
            <option value="operacao">Operações</option>
            <option value="somar">+</option>
            <option value="diminuir">-</option>
            <option value="multiplicacao">*</option>
            <option value="divisao">÷</option>
          </select>
      </div>
      <div class="col-md-2">
        <input required @change="evento => estado.NumeroTemp2 = evento.target.value" @submit="cadastraNumero02" type="number"
          placeholder="Nº">
      </div>
      <div class="col-md-1">
        <span class="ms-4">=</span>
      </div>
      <div class="col-md-2">
        <input v-model="estado.resultado" type="number" placeholder="Resultado">
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

.sub {
  text-align: center;
  font-size: 20px;
}

.text {
  text-align: center;
  font-size: 16px;
}

input {
  border-color: rgb(138, 235, 167);
  border-radius: 3px;
  text-align: center;
}

select {
  border-radius: 3px;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  background-color: rgba(77, 236, 15, 0.562);
  cursor: pointer;
}

option {
  text-align: center;
}

</style>
