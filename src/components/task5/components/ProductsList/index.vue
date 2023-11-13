<template>
  <div class="products-container">
    <laptop-item v-for="product in productsList" :key="product.id" :laptop-data="product" />
  </div>
</template>

<script>
import LaptopItem from './LaptopItem.vue'

export default {
  name: 'ProductsList',
  props: {
    productsList: {
      type: Array,
      default: () => [],
    },
  },
  components: { LaptopItem },
}
</script>

<style lang="scss" scoped>
.products-container {
  display: grid;
  gap: 1.25rem 2.5rem;
  grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
}
</style>
