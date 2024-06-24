<template>
    <div class="container mx-auto p-4">
      <button @click="fetchProducts" class="bg-blue-500 text-white px-4 py-2 rounded shadow hover:bg-blue-700 transition">
        Buscar Produtos
      </button>
      <table v-if="products.length" class="min-w-full bg-white border border-gray-300 mt-4">
        <thead>
          <tr>
            <th class="py-2 px-4 border-b">Barcode</th>
            <th class="py-2 px-4 border-b">Nome</th>
            <th class="py-2 px-4 border-b">Descrição</th>
            <th class="py-2 px-4 border-b">Categoria</th>
            <th class="py-2 px-4 border-b">Subcategoria</th>
            <th class="py-2 px-4 border-b">Preço</th>
            <th class="py-2 px-4 border-b">Altura</th>
            <th class="py-2 px-4 border-b">Largura</th>
            <th class="py-2 px-4 border-b">Peso</th>
            <th class="py-2 px-4 border-b">Comprimento</th>
            <th class="py-2 px-4 border-b">Imagens</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in products" :key="product.barcode" class="hover:bg-gray-100">
            <td class="py-2 px-4 border-b">{{ product.barcode }}</td>
            <td class="py-2 px-4 border-b">{{ product.name }}</td>
            <td class="py-2 px-4 border-b" v-html="product.description"></td>
            <td class="py-2 px-4 border-b">{{ product.category }}</td>
            <td class="py-2 px-4 border-b">{{ product.sub_category }}</td>
            <td class="py-2 px-4 border-b">{{ formatPrice(product.price) }}</td>
            <td class="py-2 px-4 border-b">{{ product.height }}</td>
            <td class="py-2 px-4 border-b">{{ product.width }}</td>
            <td class="py-2 px-4 border-b">{{ product.weight }}</td>
            <td class="py-2 px-4 border-b">{{ product.length }}</td>
            <td class="py-2 px-4 border-b">
              <img v-for="image in product.images" :src="image" :key="image" :alt="product.name" class="w-16 h-16 object-cover m-1"/>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const products = ref([])
  
  const fetchProducts = async () => {
    try {
      const response = await fetch('https://api-homolog.bonificaoficial.com/all-products')
      products.value = await response.json()
    } catch (error) {
      console.error('Erro ao buscar produtos:', error)
    }
  }
  
  const formatPrice = (price) => {
    return (price / 100).toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' })
  }
  </script>
  
  <style scoped>
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    padding: 10px;
    border: 1px solid #ddd;
  }
  th {
    background-color: #f4f4f4;
  }
  .product-image {
    max-width: 50px;
    margin: 2px;
  }
  </style>
  