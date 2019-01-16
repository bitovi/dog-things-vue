<template>
  <div class="product-list">
    <ul class="list-of-products">
      <li v-for="product in products" :key="product.id">
        <aside>
          <img class="product-image" :src="product.image" alt="The product" />
        </aside>

        <div class="product-info">
          <header>
            <h1>{{ product.name }}</h1>
          </header>
          <div class="product-desc">
            {{ product.desc }}
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import * as api from '../api';

export default {
  name: 'ProductList',
  props: {
    msg: String
  },
  data() {
    return {
      products: []
    };
  },
  mounted () {
    api.getProducts(product => {
      this.products.push(product);
    });
  }
}
</script>

<style>
.list-of-products {
  padding: 0;
  list-style-type: none;
}
.list-of-products > li {
  display: flex;
  border-top: 1px solid #DDD;
  padding-bottom: 1em;
}
.list-of-products > li > aside {
  width: 218px;
  text-align: center;
  flex: 1;
}
.list-of-products > li .product-info {
  flex: 3;
  line-height: 1.5em;
}
.list-of-products .product-image {
  max-width: 15rem;
  max-height: 10rem;
}

</style>
