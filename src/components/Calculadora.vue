<script setup>
import { reactive } from 'vue'

const obj = reactive({
  primeiroNumero: '',
  segundoNumero: '',
  operacaoMatematica: 'Somar',
  resultado: 0,
  operacoes: {
    Somar: (a, b) => a + b,
    Subtração: (a, b) => a - b,
    Multiplicação: (a, b) => a * b,
    Divisão: (a, b) => a / b
  },
})

const calcularResultado = () => {
  const { primeiroNumero, segundoNumero, operacaoMatematica } = obj;
  obj.resultado = obj.operacoes[operacaoMatematica](parseFloat(primeiroNumero), parseFloat(segundoNumero));

};
</script>

<template>

  <main>
    <h1>Calculadora Aritmética VueJS</h1>

    <form>
      <label for="primeiroNumero">Digite o primeiro numero:</label>
      <input v-model="obj.primeiroNumero" @input="calcularResultado" type="number" placeholder="0">

      <label for="segundoNumero">Digite o segundo numero:</label>
      <input v-model="obj.segundoNumero" @input="calcularResultado" type="number" placeholder="0">
    </form>
    <select v-model="obj.operacaoMatematica" @change="calcularResultado">
      <option value="Somar">Somar</option>
      <option value="Subtração">Subtração</option>
      <option value="Multiplicação">Multiplicação</option>
      <option value="Divisão">Divisão</option>
    </select>

    <p v-if="obj.resultado === 0">Resultado: 0</p>
    <p v-else>Resultado: {{ obj.resultado }}</p>
  </main>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

label {
  padding-bottom: 5px;
}

input {
  max-width: 200px;
  margin-bottom: 10px;
}
</style>