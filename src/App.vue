<script setup>

import { ref  } from 'vue'

const produto = ref([
    {
        id: 1,
        nome: 'Camiseta',
        preco: 49.90,
        qtd: 0,
    },
    {
        id: 2,
        nome: 'Calça',
        preco: 99.90,
        qtd: 0,
    },
    {
        id: 3,
        nome: 'Meia',
        preco: 9.90,
        qtd: 0,
    },
    {
        id: 4,
        nome: 'Sapato',
        preco: 199.90,
        qtd: 0,
    },
    {
        id: 5,
        nome: 'Boné',
        preco: 29.90,
        qtd: 0,
    },
    {
        id: 6,
        nome: 'Óculos',
        preco: 99.90,
        qtd: 0,
    },
    {
        id: 7,
        nome: 'Relógio',
        preco: 299.90,
        qtd: 0,
    },
    {
        id: 8,
        nome: 'Bermuda',
        preco: 79.90,
        qtd: 0,
    },
    {
        id: 9,
        nome: 'Cueca',
        preco: 19.90,
        qtd: 0,
    },
    {
        id: 10,
        nome: 'Meia',
        preco: 9.90,
        qtd: 0,
    }
])

// Carrinho
const carrinho = ref({
  items: [],
  total: 0
})
function addQtd(index) {
  produto.value[index].qtd++
  const varia = carrinho.value.items.indexOf(carrinho.value.items.find(c => c.id === produto.value[index].id))
  if (varia != -1) {
    carrinho.value.total -= carrinho.value.items[varia].total
    carrinho.value.items[varia].total = ++carrinho.value.items[varia].qtd * carrinho.value.items[varia].preco
    carrinho.value.total += (carrinho.value.items[varia].total)

  }
}
function subQtd(index) {
  
  const varia = carrinho.value.items.indexOf(carrinho.value.items.find(c => c.id === produto.value[index].id))
  if (produto.value[index].qtd > 0) {
      produto.value[index].qtd--
  }
  if (varia != -1) {
    carrinho.value.total -= carrinho.value.items[varia].total
    carrinho.value.items[varia].total = --carrinho.value.items[varia].qtd * carrinho.value.items[varia].preco
    carrinho.value.total += (carrinho.value.items[varia].total)
  }
}

function cleanCart(){
carrinho.value.items = []
carrinho.value.total = 0
}

function addToCart(produto) {
  if (produto.qtd === 0){
    return false
  } else {
    carrinho.value.items.push({
      id: produto.id,
      nome: produto.nome,
      preco: produto.preco,
      qtd: produto.qtd,
      total: produto.preco * produto.qtd
    });
    carrinho.value.total = (carrinho.value.total + (produto.preco * produto.qtd))
  }
}


</script>

<template>
  <div>
    <header>
      <h1> Shopping </h1>
    </header>
    <br>
    <main>
      <div v-for="(produto, index) in produto" :key="produto.id" class="produto">

        <div class="produtos">
          <b> {{ produto.id }} - {{ produto.nome }} </b>
          <br>
          <h6>Preço: {{ produto.preco }}</h6>
          <h6>Quantidade: {{ produto.qtd }}</h6>

          <button type="button" @click="subQtd(index)">-</button>
          <button type="button" @click="addQtd(index)">+</button>
          <button class="add" type="button" @click="addToCart(produto)">Adicionar</button>
        </div>
      </div>
    </main>  
    <div>
      <h1 class="h1">  
        Carrinho
      </h1>
      <div v-for="(item, index) in carrinho.items" :key="item.id" class="col-3">
        <div class="produtos">
          <h2> {{ item.nome }} <h6> Quantidade: {{ item.qtd }} | Total: {{ item.qtd * item.preco }}</h6> </h2>
        </div>
      </div>
    </div>
    <h4 style="margin-top: 1em;">Valor Total: {{ carrinho.total }}</h4>
    <button class="add" type="button" @click="cleanCart()">Limpar Carrinho</button>
  </div>
</template>

<style scoped>

main {
  display: flex; 
  gap: 16px;
}

.h1 {
  margin: 1em 0 0 0;
}
.produto{
  background-color: rgb(119, 119, 119);
  padding: 25px;
  color: white;
  border-radius: 5px;
  width: 100%;
  margin-top: 30px;
}
button {
  background-color: rgb(8, 46, 77);
  border-radius: 5px;
  color: white;
  margin: 2px 1px;
  cursor: pointer;
  border-radius: 20px;
  border: none;
}
button.add {
  font-size: 1em;
  background-color: rgb(8, 46, 77);
  border-radius: 5px;
  color: white;
  padding: 10px 20px;
  border-radius: 20px;
  border: none;
}
h1 {
  text-align: center;
}
h6 {
  padding: auto;
}
</style>

