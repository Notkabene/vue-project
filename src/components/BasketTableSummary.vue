<script setup>
import { computed, inject } from 'vue'

const totalTax = computed(() => {
  return totalPrice.value / 10
})

const { totalPrice, increaseItemQuantity, removeItem, summarySubtotalProduct } = inject('actionTable')

</script>

<template>
  <tr>
    <td colspan="5">
      <div class="basket-table__summary">
        <p class="basket-table__total">Total <b>${{ totalPrice }},00</b></p>
        <p>Tax ${{ totalTax }}</p>
      </div>
    </td>
  </tr>
</template>

<style scoped>
.basket-table__summary {
  text-align: right;
}

.basket-table__total {
  font-size: 1.4rem;
}

</style>
