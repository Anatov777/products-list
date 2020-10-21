<template>
  <div id="products_section">
    <div class="products_page pg_0">
      <Product
        v-for="(item, index) in products"
        :key="item.productId + '%' + index"
        :prodData="item"
      />
    </div>
  </div>
</template>

<script>
import Product from "./Product.vue";

export default {
  name: "ProductList",
  components: {
    Product,
  },
  data() {
    return {
      products: this.getProducts(),
    };
  },
  methods: {
    getProducts() {
      return require("@/products.json");
    },
  },
};
</script>

