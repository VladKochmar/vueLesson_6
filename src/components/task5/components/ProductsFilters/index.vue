<template>
  <aside class="sidebar">
    <div class="filter-container">
      <h4 class="filter-container__title">Продавець</h4>
      <div class="checkbox" v-for="(seller, index) in sellersList" :key="index">
        <label class="checkbox__label">
          <input type="checkbox" :value="seller" @change="$emit('checkSeller', seller)" />
          {{ seller }}
        </label>
      </div>
    </div>
    <div class="filter-container">
      <h4 class="filter-container__title">Бренд</h4>
      <input type="text" v-model="currentBrand" class="input" />
    </div>
    <div class="filter-container">
      <h4 class="filter-container__title">Алфавітний вказівник</h4>
      <div class="checkbox" v-for="(brand, index) in filteredBrandsList" :key="index">
        <label class="checkbox__label">
          <input type="checkbox" :value="brand" @change="$emit('checkBrand', brand)" />
          {{ brand }}
        </label>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'ProductsFilters',
  props: {
    sellersList: {
      type: Array,
      default: () => [],
    },
    brandsList: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      currentBrand: null,
    }
  },
  computed: {
    filteredBrandsList() {
      const filteredBrands = this.brandsList.filter((brand) => {
        if (brand && this.currentBrand) return brand.toLowerCase().includes(this.currentBrand.toLowerCase())
        else return false
      })
      return filteredBrands.length ? filteredBrands : this.brandsList
    },
  },
}
</script>

<style lang="scss" scoped>
.sidebar {
  align-self: flex-start;
  border: 2px solid #fff;
  padding: 1.25rem 0.625rem;
}
.filter-container {
  padding: 0.9375rem 0;
  // .filter-container__title
  &__title {
    &:not(:last-child) {
      margin-bottom: 1.25rem;
    }
  }
}
.checkbox {
  &:not(:last-child) {
    margin-bottom: 0.625rem;
  }
  // .checkbox__label
  &__label,
  input {
    cursor: pointer;
  }
}
</style>
