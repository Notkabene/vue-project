<script setup>
import {computed, reactive} from "vue";

const basket = reactive([
  {
    id: 1,
    name: 'Blue Flower Print Crop Top',
    color: 'Yellow',
    size: 'M',
    price: 29.0,
    quantity: 1,
    imageUrl: './assets/crop-top.png',
  },
  {
    id: 2,
    name: 'Levender Hoodie',
    color: 'Levender',
    size: 'XXL',
    price: 119.0,
    quantity: 1,
    imageUrl: './assets/hoodie.png',
  },
  {
    id: 3,
    name: 'Black Sweatshirt',
    color: 'Black',
    size: 'XXL',
    price: 123.0,
    quantity: 1,
    imageUrl: './assets/sweatshirt.png',
  },

])

const totalPrice = computed(() => {
  let total = 0;
  basket.forEach((item) => {
    total = total + (item.price * item.quantity);
  })
  return total;
})

const totalTax = computed(() => {
  return totalPrice.value / 10;
})

function summarySubtotalProduct(product) {
  return product.quantity * product.price;
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

</script>

<template>
  <div class="container basket">
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

        <tr v-for="product in basket" :key="product.id">
          <td>
            <div class="basket-item">
              <div class="basket-item__image">
                <img :src="product.imageUrl" :alt="product.name"/>
              </div>
              <div class="basket-item__info">
                <h2 class="basket-item__info-h2">{{ product.name }}</h2>
                <p class="basket-item__info-p">Color: {{ product.color }}</p>
                <p class="basket-item__info-p">Size: {{ product.size }}</p>
              </div>
            </div>
          </td>
          <td>
            <p class="basket-item__price">${{ product.price }},00</p>
          </td>
          <td>
            <div class="basket-item__quantity">
              <button class="quantity-button" @click="decreaseItemQuantity(product)">–</button>
              <input type="number" min="1" :value="product.quantity"/>
              <button class="quantity-button" @click="increaseItemQuantity(product)">+</button>
            </div>
          </td>
          <td>
            <p class="basket-item__price">$ {{ summarySubtotalProduct(product) }},00 </p>
          </td>
          <td>
            <button class="btn btn-delete" aria-label="Удалить" @click="removeItem(product.id)">
              <svg
                class="w-6 h-6 text-gray-800 dark:text-white"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                fill="none"
                viewBox="0 0 24 24"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M5 7h14m-9 3v8m4-8v8M10 3h4a1 1 0 0 1 1 1v3H9V4a1 1 0 0 1 1-1ZM6 7h12v13a1 1 0 0 1-1 1H7a1 1 0 0 1-1-1V7Z"
                />
              </svg>
            </button>
          </td>
        </tr>
      </template>
      <tr v-else>
        <td>No items</td>
      </tr>

      <tr v-if="basket.length">
        <td colspan="5">
          <div class="basket-table__summary">
            <p class="basket-table__total">Total <b>${{ totalPrice }},00</b></p>
            <p>Tax ${{ totalTax }}</p>
          </div>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
@import "App.css";
</style>
