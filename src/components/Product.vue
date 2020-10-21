<template>
  <div class="product product_horizontal">
    <span class="product_code">Код: {{ prodData.code.replace(/^0+/, '') }}</span>
    <div class="product_status_tooltip_container">
      <span class="product_status">Наличие</span>
    </div>
    <div class="product_photo">
      <a href="#" class="url--link product__link">
        <img :src="prodData.primaryImageUrl" />
      </a>
    </div>
    <div class="product_description">
      <a href="#" class="product__link">{{ prodData.title }}</a>
    </div>
    <div class="product_tags hidden-sm">
      <p>Могут понадобиться:</p>
      &nbsp;
      <template v-for="(assocProduct, index) in prodData.assocProducts.split(';')">
        <a :key="prodData.productId + index" href="#" class="url--link">{{
          formatAssoc(assocProduct, prodData.assocProducts.split(";"))
        }}</a>
      </template>
    </div>
    <div class="product_units">
      <div class="unit--wrapper">
        <div
          class="unit--select"
          :class="priceType === 'meter' ? 'unit--active' : ''"
          v-on:click="priceType = 'meter'"
        >
          <p class="ng-binding">За м. кв.</p>
        </div>
        <div
          class="unit--select"
          :class="priceType === 'pack' ? 'unit--active' : ''"
          v-on:click="priceType = 'pack'"
        >
          <p class="ng-binding">За упаковку</p>
        </div>
      </div>
    </div>
    <p class="product_price_club_card">
      <span class="product_price_club_card_text">По карте<br />клуба</span>
      <span class="goldPrice">{{
        (totalPrice[0] * productNumber).toFixed(2)
      }}</span>
      <span class="rouble__i black__i">
        <svg
          version="1.0"
          id="rouble__b"
          xmlns="http://www.w3.org/2000/svg"
          x="0"
          y="0"
          width="30px"
          height="22px"
          viewBox="0 0 50 50"
          enable-background="new 0 0 50 50"
          xml:space="preserve"
        >
          <use
            xmlns:xlink="http://www.w3.org/1999/xlink"
            xlink:href="#rouble_black"
          ></use>
        </svg>
      </span>
    </p>
    <p class="product_price_default">
      <span class="retailPrice">{{
        (totalPrice[1] * productNumber).toFixed(2)
      }}</span>
      <span class="rouble__i black__i">
        <svg
          version="1.0"
          id="rouble__g"
          xmlns="http://www.w3.org/2000/svg"
          x="0"
          y="0"
          width="30px"
          height="22px"
          viewBox="0 0 50 50"
          enable-background="new 0 0 50 50"
          xml:space="preserve"
        >
          <use
            xmlns:xlink="http://www.w3.org/1999/xlink"
            xlink:href="#rouble_gray"
          ></use>
        </svg>
      </span>
    </p>
    <div class="product_price_points">
      <p class="ng-binding">Можно купить за баллы</p>
    </div>
    <div class="list--unit-padd"></div>
    <div class="list--unit-desc">
      <div class="unit--info">
        <div class="unit--desc-i"></div>
        <div class="unit--desc-t">
          <p>
            <span class="ng-binding">Продается упаковками:</span>
            <span class="unit--infoInn"
              >{{ prodData.unitRatio }} упак. = {{ prodData.unitRatioAlt.toFixed(2) }}
              {{ prodData.unitAlt }}
            </span>
          </p>
        </div>
      </div>
    </div>
    <div class="product__wrapper">
      <div class="product_count_wrapper">
        <div class="stepper">
          <input
            class="product__count stepper-input"
            type="text"
            v-model="productNumber"
          />
          <span class="stepper-arrow up" v-on:click="productNumber++"></span>
          <span class="stepper-arrow down" v-on:click="productNumber--"></span>
        </div>
      </div>
      <span
        class="btn btn_cart"
        data-url="/cart/"
        data-product-id="9bf0afd7-5190-11e5-b9a9-00259036a192"
      >
        <svg class="ic ic_cart">
          <use
            xmlns:xlink="http://www.w3.org/1999/xlink"
            xlink:href="#cart"
          ></use>
        </svg>
        <span class="ng-binding" :data-product-id="prodData.productId"
          >В корзину</span
        >
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: ["prodData"],
  data() {
    return {
      productNumber: '1',
      priceType: 'meter',
    };
  },
  watch: {
    productNumber: function () {
      if (this.productNumber < 1) {
        this.productNumber = 1;
      }
    },
    priceType: function () {
      if (this.priceType === "pack") {
        this.totalPrice[0] = this.prodData.priceGoldAlt.toFixed(2);
        this.totalPrice[1] = this.prodData.priceRetailAlt.toFixed(2);
      } else if (this.priceType === "meter") {
        this.totalPrice[0] = this.prodData.priceGold.toFixed(2);
        this.totalPrice[1] = this.prodData.priceRetail.toFixed(2);
      }
    },
  },
  computed: {
    totalPrice: function () {
      let tmpArray = [];
      tmpArray.push(this.prodData.priceGold.toFixed(2));
      tmpArray.push(this.prodData.priceRetail.toFixed(2));
      return tmpArray;
    },
  },
  methods: {
    formatAssoc(elem, arr) {
      if (elem === arr[arr.length - 2]) {
        return elem + ".";
      } else if (elem === "") {
        return elem;
      } else {
        return elem + ",";
      }
    },
    // imgUrlModif(imgUrl) {
    //   let tmpArr = imgUrl.split('.')
    //   tmpArr.splice(-1, 0, '_220x220_1.');
    //   return tmpArr.join('');
    // },
  },
};
</script>