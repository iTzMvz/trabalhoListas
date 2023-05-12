<script setup>
import { ref } from 'vue'

const verCarrinho = ref(false)
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
  },
  {
    id: 5,
    nome: 'Casaco',
    preco: 99.99,
    quantidade: 0
  },
  {
    id: 6,
    nome: 'Moletom',
    preco: 149.99,
    quantidade: 0
  },
  {
    id: 7,
    nome: 'Sapato',
    preco: 69.99,
    quantidade: 0
  },
  {
    id: 8,
    nome: 'Cinto',
    preco: 29.99,
    quantidade: 0
  },
  {
    id: 9,
    nome: 'Sapato',
    preco: 69.99,
    quantidade: 0
  }
])

function addCarrinho(id, nome, quantidade, preco) {
  if (quantidade == 0) {
    alert(erroQnt.value)
  } else {
    carrinho.value.push({ id, nome, quantidade, preco })
    calculaValorTotal()
  }
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
function limpaCarrinho() {
  if (carrinho.value.length > 0) {
    carrinho.value = []
    valorTotal.value = 0
  } else alert('O carrinho já está vazio')
}

function quantItens() {
  if(carrinho[carrinho.findIndex(produto => produto.id == -1)]){
    carrinho.push()
  }
}
</script>
<template>
  <ul>
    <div class="produtos">
      <li v-for="(produto, i) in listaProdutos" :key="i">
        <div>{{ produto.nome }}</div>
        <div>
          {{ produto.preco.toLocaleString('pt-br', { style: 'currency', currency: 'BRL' }) }}
        </div>
        <div>Quantidade: {{ produto.quantidade }}</div>
        <button @click="addCarrinho(produto.id, produto.nome, produto.quantidade, produto.preco), produto.quantidade = 0">
          Adicionar
        </button>
        <div>
          <button @click="produto.quantidade++" id="mais">+</button>
          <button v-if="produto.quantidade > 0" @click="produto.quantidade--" id="menos">-</button>
        </div>
      </li>
    </div>
  </ul>
  <ul>
    <button @click="verCarrinho = !verCarrinho" style="margin-left: 20px" v-if="carrinho.length > 0">
      Ver carrinho
    </button>
    <div v-if="verCarrinho">
      <div>
        <button @click="limpaCarrinho()" style="margin-left: 20px" v-if="carrinho.length > 0">
          Limpar carrinho
        </button>
      </div>
      <div class="carrinho">
        <div v-if="valorTotal > 0">
          Valor total:
          {{ valorTotal.toLocaleString('pt-br', { style: 'currency', currency: 'BRL' }) }}
        </div>
        <li v-for="(produto, i) in carrinho" :key="i">
          <div>{{ produto.nome }}</div>
          <div>
            {{ produto.preco.toLocaleString('pt-br', { style: 'currency', currency: 'BRL' }) }}
          </div>
          <div>Quantidade: {{ produto.quantidade }}</div>
        </li>
      </div>
    </div>
  </ul>
</template>
<style scoped>
button {
  margin: 5px;
  border-radius: 10px;
  font-weight: bold;
  background-color: rgb(231, 213, 130);
  box-shadow: 3px 4px 5px rgb(133, 117, 45);
}

.produtos {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: start;
}

.carrinho {
  display: flex;
  flex-direction: column;
}

li {
  margin-right: 20px;
  margin-left: 20px;
  list-style: none;
}

#mais {
  background-color: rgb(161, 211, 231);
  box-shadow: 2px 3px 5px rgb(54, 80, 90);
}

#menos {
  padding-right: 6px;
  padding-left: 6px;
  background-color: rgb(230, 43, 32);
  box-shadow: 2px 3px 5px rgb(116, 26, 22);
}
</style>
