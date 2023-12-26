<script>
export default {
  data() {
    return {
      products: [],
    };
  },
  computed: {
    productCategory() {
      if (this.products.category === "men's clothing") {
        return "men-clothing";
      } else if (this.products.category === "women's clothing") {
        return "women-clothing";
      } else {
        return "unavailable";
      }
    },
  },
  mounted() {
    this.fetchProduct();
  },
  methods: {
    getRating() {
      if (this.products.rating) {
        return this.products.rating.rate;
      } else {
        return "N/A";
      }
    },
    async fetchProduct() {
      try {
        const response = await fetch("https://fakestoreapi.com/products/1");
        const data = await response.json();
        this.products = data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
  },
};
</script>

<template>
  <div :class="productCategory">
    <div class="hero"><img src="./assets/img/bg-pattern.svg" alt="" /></div>
    <div class="product">
      <div class="img-prod">
        <img :src="products.image" alt="" height="480px" width="350px" />
      </div>
      <div class="detail-prod">
        <h1>
          {{ products.title }}
        </h1>
        <div class="cat-rat">
          <p>
            {{ products.category }}
          </p>
          <p>
            {{ getRating() }}
            /5 <span class="stars"></span>
          </p>
        </div>
        <hr />
        <p class="desc">
          {{ products.description }}
        </p>
        <hr />
        <p>${{ products.price }}</p>
        <div class="buy">Buy</div>
        <div class="next">Next Product</div>
      </div>
    </div>
  </div>
</template>

<style>
@import "./assets/css/base.css";
</style>
