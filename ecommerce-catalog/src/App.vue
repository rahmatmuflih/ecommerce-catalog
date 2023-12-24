<script>
export default {
  name: "Hello World",
  props: {
    msg: String,
  },
  data() {
    return {
      foods: ["Pizza", "French Fries", "Hotdog", "Tacos", "Spaghetti"],
    };
  },
};
</script>

<template>
  <main>
    <ul v-for="food in foods" v-bind:key="food">
      {{
        food
      }}
    </ul>
  </main>
</template>

<style scoped>
h1 {
  color: red;
}
</style>
