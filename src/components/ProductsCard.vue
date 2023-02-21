<template>
  <div
    class="products-content-items"
    v-for="product in products"
    :key="product.idx"
  >
    <h2>Brand : {{ product.brand }}</h2>
    <div><img :src="product.images[0]" alt="" /></div>
    <h3>{{ product.title }}</h3>
    <p>{{ product.description }}</p>
    <div class="products-content-items-info">
      <span>{{ product.price }} $</span>
      <span>{{ product.rating }}</span>
      <span>{{ product.discountPercentage }}</span>
    </div>
  </div>
</template>
<script>
export default {
  props: ["products"],
};
</script>
<style lang="scss">
</style>