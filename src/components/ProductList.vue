<template>
  <div id="products_section">
    <div class="products_page pg_0">
      <!-- <div
        class="product product_horizontal"
        v-for="(item, index) in products"
        :key="item.productId + '%' + index"
      > -->
        <Product v-for="(item, index) in products" :key="item.productId + '%' + index" :prodData="item"/>
      <!-- </div> -->
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
      // productNumber: '1',
      // priceType: 'meter',
    };
  },
  // watch: {
  //   productNumber: function () {
  //     if (this.productNumber < 1) {
  //       this.productNumber = 1;
  //     }
  //   },
  //   priceType: function () {
  //     if (this.priceType === 'pack') {
  //       console.log(event);
  //     }
  //   }
  // },
  methods: {
    getProducts() {
      return require("@/products.json");
    },
    // formatAssoc(elem, arr) {
    //   if (elem === arr[arr.length - 2]) {
    //     return elem + ".";
    //   } else if (elem === "") {
    //     return elem;
    //   } else {
    //     return elem + ",";
    //   }
    // },


    // imgUrlModif(imgUrl) {
    //   let tmpArr = imgUrl.split('.')
    //   tmpArr.splice(-1, 0, '_220x220_1.');
    //   return tmpArr.join('');
    // },
  },
};
</script>

