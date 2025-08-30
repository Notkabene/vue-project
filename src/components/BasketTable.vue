<script setup>
import BasketTableSummary from '@/components/BasketTableSummary.vue'
import BasketTableItem from '@/components/BasketTableItem.vue'

defineProps({
  basket: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <table class="basket-table">
    <thead class="basket-table__header">
    <tr>
      <th>Product Details</th>
      <th>Price</th>
      <th>Quantity</th>
      <th>Subtotal</th>
      <th>Action</th>
    </tr>
    </thead>
    <tbody class="basket-table__body">
    <template v-if="basket.length">
      <BasketTableItem v-for="product in basket" :key="product.id" :product="product" />
    </template>
    <tr class="basket-table__empty" v-else>
      <td>No items</td>
    </tr>
    <BasketTableSummary v-if="basket.length" />
    </tbody>
  </table>
</template>

<style scoped>
.basket-table {
  width: 100%;
  border-collapse: collapse;
}

.basket-table__header {
  background-color: #3c4242;
  color: #fff;
  font-weight: 400;
  text-transform: uppercase;
}

.basket-table__header th {
  padding: 2rem 1rem;
  font-weight: 400;
  text-align: center;
  border: 0;
}

.basket-table__header th:first-child {
  text-align: left;
  padding-left: 5rem;
}

.basket-table__header th:last-child {
  padding-right: 5rem;
}

.basket-table__empty {
  text-align: center;
  color: #a7a7a7;
}
</style>
