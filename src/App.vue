<script setup>
import { ref } from 'vue'

const erroQnt = ref('Adicione o produto primeiro antes de colocar no carrinho')
const carrinho = ref([])
const listaProdutos = ref([
  {
    id: 1,
    nome: 'Calça',
    preco: 59.99,
    quantidade: 0
  },
  {
    id: 2,
    nome: 'Camiseta',
    preco: 49.99,
    quantidade: 0
  },
  {
    id: 3,
    nome: 'Tênis',
    preco: 89.99,
    quantidade: 0
  },
  {
    id: 4,
    nome: 'Bermuda',
    preco: 39.99,
    quantidade: 0
  }
])

function addCarrinho(produto) {
  if (produto.quantidade == 0) {
   alert(erroQnt.value)
  } else {
    carrinho.value.push(produto.id, produto.nome, produto.preco, produto.quantidade)
    calculaValorTotal()
  }
  produto.quantidade = 0
}

const valorTotal = ref(0)

function calculaValorTotal() {
  valorTotal.value = 0
  if (carrinho.value.length > 0) {
    for (let item of carrinho.value) {
      valorTotal.value = valorTotal.value + item.preco * item.quantidade
    }
  }
}
</script>
<template>
  <ul>
    <li v-for="(produto, i) in listaProdutos" :key="produto.id">
      <div>{{ produto.nome }}</div>
      <div>
        {{ produto.preco.toLocaleString('pt-br', { style: 'currency', currency: 'BRL' }) }}
      </div>
      <div>Quantidade: {{ produto.quantidade }}</div>
      <button @click="addCarrinho(produto)">Adicionar</button>
      <button @click="produto.quantidade++" style="background-color: rgb(161, 211, 231)">+</button>
      <button v-if="produto.quantidade > 0" @click="produto.quantidade--" style="background-color: rgb(230, 43, 32)">
        -
      </button>
      <div></div>
    </li>
  </ul>
  <div>{{ carrinho }}</div>
</template>
<style scoped>
button {
  margin: 5px;
  border-radius: 10px;
  font-weight: bold;
  background-color: rgb(231, 213, 130);
}
</style>
