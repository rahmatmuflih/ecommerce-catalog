<script>
export default {
  data() {
    return {
      products: [],
      maxStars: 5,
      currentProductIndex: 1,
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
    filledStars() {
      const filledCount = Math.round(
        this.products.rating ? this.products.rating.rate : 0
      );
      return Array.from({ length: filledCount }, (_, index) => index);
    },
    emptyStars() {
      const emptyCount =
        this.maxStars -
        Math.round(this.products.rating ? this.products.rating.rate : 0);
      return Array.from({ length: emptyCount }, (_, index) => index);
    },
  },
  mounted() {
    this.fetchProduct(this.currentProductIndex);
  },
  methods: {
    async fetchProduct(index) {
      try {
        const response = await fetch(`https://fakestoreapi.com/products/${index}`);
        const data = await response.json();
        if (Object.keys(data).length === 0) {
          console.error("Empty response from the server");
          return;
        }
        this.products = data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
    nextProduct(){
      this.currentProductIndex++;
      if(this.currentProductIndex > 20){
        this.currentProductIndex = 1;
      }
      this.fetchProduct(this.currentProductIndex);
    }
  },
};
</script>

<template>
  <div :class="productCategory">
    <div class="hero"><img src="./assets/img/bg-pattern.svg" alt="" /></div>
    <div class="product">
      <div class="unavailable-product">
        <p>This product is unavailable to show</p>
        <div class="next" @click="nextProduct">Next Product</div>
      </div>
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
            {{ products.rating ? products.rating.rate : "N/A" }}
            /5 <div v-for="star in filledStars" :key="star" class="stars">
            </div><div v-for="star in emptyStars" :key="star" class="stars-off"></div>
          </p>
        </div>
        <hr />
        <p class="desc">
          {{ products.description }}
        </p>
        <hr class="bottom-hr" />
        <p>${{ products.price }}</p>
        <div class="buy">Buy</div>
        <div class="next" @click="nextProduct">Next Product</div>
      </div>
    </div>
  </div>
</template>

<style>
@import "./assets/css/base.css";
</style>
