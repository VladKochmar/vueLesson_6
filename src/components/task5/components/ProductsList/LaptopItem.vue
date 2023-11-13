<template>
  <a :href="laptopData.link" class="card">
    <div class="card__image"><img :src="laptopData.imgSrc" :alt="laptopData.title" /></div>
    <h3 class="card__title">{{ laptopData.title }}</h3>
    <div class="card__old-price">{{ laptopData.oldPrice }} ₴</div>
    <div class="card__price">{{ laptopData.price }} ₴</div>
  </a>
</template>

<script>
export default {
  name: 'LaptopItem',
  props: {
    laptopData: {
      type: Object,
      default: () => ({}),
    },
  },
}
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  flex-direction: column;
  // .card__image
  &__image {
    display: grid;
    align-items: center;
    background-color: #fff;
    flex: 1 1 auto;
    img {
      max-width: 100%;
    }
    &:not(:last-child) {
      margin-bottom: 2rem;
    }
  }
  // .card__title
  &__title {
    font-size: 1.125rem;
    line-height: 1.25;
    &:not(:last-child) {
      margin-bottom: 1rem;
    }
  }
  // .card__old-price
  &__old-price {
    color: gray;
    font-size: 1.25rem;
    text-decoration: line-through;
    &:not(:last-child) {
      margin-bottom: 1rem;
    }
  }
  // .card__price
  &__price {
    color: red;
    font-size: 1.75rem;
    line-height: 1.5;
  }
}
</style>
