<script setup>
import { computed, provide, reactive } from 'vue'
import BasketTable from '@/components/BasketTable.vue'

const basket = reactive([
  {
    id: 1,
    name: 'Blue Flower Print Crop Top',
    color: 'Yellow',
    size: 'M',
    price: 29.0,
    quantity: 1,
    imageUrl: './assets/crop-top.png'
  },
  {
    id: 2,
    name: 'Levender Hoodie',
    color: 'Levender',
    size: 'XXL',
    price: 119.0,
    quantity: 1,
    imageUrl: './assets/hoodie.png'
  },
  {
    id: 3,
    name: 'Black Sweatshirt',
    color: 'Black',
    size: 'XXL',
    price: 123.0,
    quantity: 1,
    imageUrl: './assets/sweatshirt.png'
  }

])

const totalPrice = computed(() => {
  let total = 0
  basket.forEach((item) => {
    total = total + (item.price * item.quantity)
  })
  return total
})

function summarySubtotalProduct(product) {
  return product.quantity * product.price
}

function increaseItemQuantity(product) {
  return product.quantity++
}

function decreaseItemQuantity(product) {
  return product.quantity > 1 ? product.quantity-- : product.quantity
}

function removeItem(productId) {
  basket.splice(0, basket.length, ...basket.filter(item => item.id !== productId))
}

provide('actionTable', {
  totalPrice,
  summarySubtotalProduct,
  increaseItemQuantity,
  decreaseItemQuantity,
  removeItem,
})

</script>

<template>
  <div class="container basket">
    <BasketTable :basket="basket" />
  </div>
</template>

<style scoped>
body {
  background-color: #f0f0f0;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
  Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif, sans-serif;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  background-color: #fff;
}
</style>
