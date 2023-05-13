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

</script>
<template>
  <h1>Mvz's Shop</h1>
  <ul>
    <div class="produtos">
      <li v-for="(produto, i) in listaProdutos" :key="i" class="item">
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
    <div class="card">
        <button @click="limpaCarrinho()" v-if="carrinho.length > 0">
          Limpar carrinho
        </button>
    </div>
     <div v-if="valorTotal > 0" style="text-align: center;">
         <h3> Valor total:
          {{ valorTotal.toLocaleString('pt-br', { style: 'currency', currency: 'BRL' }) }}
        </h3>
        </div>
      <div class="carrinho">
        <li v-for="(produto, i) in carrinho" :key="i" class="itemCarrinho">
          <div>{{ produto.nome }}</div>
          <div>
            {{ produto.preco.toLocaleString('pt-br', { style: 'currency', currency: 'BRL' }) }}
          </div>
          <div>Quantidade: {{ produto.quantidade }}</div>
        </li>
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
  justify-content: center;
  width: 600px;
  margin: auto;
}
.card{
  display: flex;
  flex-direction: column;
  align-items: center;

}
.carrinho {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 400px;
  margin: auto;
}
.item{
  margin: 2% 20px;
  list-style: none;
  background-color: #0D0D0D;
  color: white;
  padding: 20px;
  border-radius: 15px;
}

.itemCarrinho{
  list-style: none;
  background-color: #0D0D0D;
  color: white;
  padding: 20px;
  border-radius: 15px;
  margin: 5px 20px;

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
h1{
  text-align: center;
}
</style>
