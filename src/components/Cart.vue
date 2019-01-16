<template>
  <a href="/cart" class="cart-link">
    <img class="cart-img" src="../assets/shopping-cart.svg" alt="shopping cart" />
    <span id="cart-count" class="cart-count">{{ count }}</span>
  </a>
</template>

<script>
import * as api from '../api';

export default {
  name: 'Cart',
  data() {
    return {
      count: 0
    };
  },
  async mounted () {
    let cart = await api.getCart();
    this.count = cart.count;
  }
}
</script>

<style>
</style>