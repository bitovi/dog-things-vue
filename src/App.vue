<template>
  <div id="app">
    <header class="App-header">
      <div class="header-left">
      <h1>Dog Things</h1>
      </div>

      <div c="header-right">
        <Cart />
      </div>
    </header>

    <main>
      <p v-if="isCart">Cart stuff here</p>
      <section class="product-page" v-else>
        <aside class="sideoptions">
          <h1>Categories</h1>
          <ul>
            <li>Bones</li>
            <li>Food brands</li>
          </ul>
        </aside>
        <ProductList/>
        <!-- ProductList here -->
      </section>
    </main>
  </div>
</template>

<script>
import Cart from './components/Cart.vue'
import ProductList from './components/ProductList.vue'

export default {
  name: 'app',
  components: {
    Cart, ProductList
  },
  data() {
    return {
      page: 'products'
    }
  },
  computed: {
    isCart() {
      return this.page === 'cart';
    }
  }
}
</script>

<style>
body {
  font-family: "Helvetica Neue-Light", "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif;
  font-weight: 300;
}
header {
  display: flex;
  margin-right: 2em;
}
header .header-left,
header .header-right {
  flex: 1;
}
header .header-right {
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
.product-page {
  display: flex;
  margin: 0 4rem;
}
.product-page .sideoptions {
  flex: 1;
}
.product-page .sideoptions ul {
  padding: 0;
  list-style-type: none;
  line-height: 1.5rem;
}
.product-page product-list {
  flex: 5;
}

</style>
