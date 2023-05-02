<script setup>
import { ref } from 'vue';

const listaProdutos = ref([
    {
        id: 1,
        name: 'Item 1',
        preco: 0,
        quantidade: 0
    },
    {
        id: 2,
        name: 'Item 2',
        preco: 0,
        quantidade: 0
    },
    {
        id: 3,
        name: 'Item 3',
        preco: 0,
        quantidade: 0
    }
])
</script>
<template>
    <ul>
        <li v-for="(produto, id) in listaProdutos" :key="produto.id">{{ produto.name }} {{ produto.quantidade }}<button @click="produto.quantidade++">+</button> <button @click="produto.quantidade--">-</button></li>
    </ul>
</template>
