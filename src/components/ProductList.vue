<template>
  <ul class="list-of-products horizontal">
    <li v-for="product in products" :key="product.id">
      <aside>
        <img class="product-image" :src="product.image" alt="The product" />
      </aside>

      <div class="product-info">
        <h2>{{ product.name }}</h2>
        <div class="product-desc">
          {{ product.desc }}
        </div>
      </div>
    </li>
  </ul>
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
      if(!this.products.length && window.parent) {
        window.parent.postMessage("first-item", "*");
      }

      this.products.push(product);
    }).then(() => {
      if(window.parent) {
        window.parent.postMessage("last-item", "*");
      }
    });
  }
}
</script>

<style>
product-list {
  display: block;
}

.list-of-products {
  padding: 0;
  list-style-type: none;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  grid-gap: 80px;
  flex: 1 1;
}

.list-of-products.horizontal {
  grid-template-columns: none;
  grid-gap: 30px;
}

.list-of-products > li {
  display: flex;
  flex-direction: column;
  background: white;
  padding: 2em;
  box-shadow: 0px 3px 0px rgba(0, 0, 0, .2);
}

.list-of-products.horizontal > li {
  flex-direction: row;
  padding: 1em;
}

.list-of-products > li:hover {
  box-shadow: 0px 10px 30px rgba(0, 0, 0, .2);
  border-top: 8px solid var(--mainColor);
  cursor: pointer;
  transition-property: box-shadow;
  transition-duration: 500ms;
  transition-timing-function: ease-in;
}

.list-of-products > li:hover .product-info h2 {
  color: var(--fontColorLinks);
}

.list-of-products > li > aside {
  width: 100%;
  height: 190px;
  display: flex;
  justify-content: center;
}

.list-of-products.horizontal > li > aside {
  height: 115px;
  flex: 1;
}

.list-of-products > li .product-info {
  line-height: 1.5em;
}

.list-of-products.horizontal > li > .product-info {
  height: 105px;
  overflow: hidden;
  flex: 3;
}

.list-of-products .product-image {
  max-height: 100%;
}
.list-of-products > li .product-info h2 {
  color: var(--fontColorTitles);
}
</style>
