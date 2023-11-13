<template>
  <div class="products-manager">
    <products-filters
      :sellers-list="sellersList"
      :brands-list="brandsList"
      @check-seller="onCheckSeller"
      @check-brand="onCheckBrand"
    />
    <products-list :products-list="filteredProductsList" />
  </div>
</template>

<script>
import ProductsFilters from './components/ProductsFilters/'
import ProductsList from './components/ProductsList/'

export default {
  name: 'ProductsManage',
  components: {
    ProductsFilters,
    ProductsList,
  },
  props: {
    productsList: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      checkedSellersList: [],
      checkedBrandsList: [],
    }
  },
  computed: {
    brandsList() {
      return [...new Set(this.productsList.map((product) => product.brand))]
    },
    sellersList() {
      return [...new Set(this.productsList.map((product) => product.seller))]
    },

    filteredProductsList() {
      if (this.checkedSellersList.length === 0 && this.checkedBrandsList.length === 0) {
        return this.productsList
      } else {
        return this.productsList.filter((product) => {
          const filteredByBrands = this.checkedBrandsList.length === 0 || this.checkedBrandsList.includes(product.brand)
          const filteredBySellers =
            this.checkedSellersList.length === 0 || this.checkedSellersList.includes(product.seller)

          return filteredByBrands && filteredBySellers
        })
      }
    },
  },
  methods: {
    onCheckSeller(checkedSeller) {
      if (this.checkedSellersList.includes(checkedSeller))
        this.checkedSellersList = this.checkedSellersList.filter((seller) => seller !== checkedSeller)
      else this.checkedSellersList.push(checkedSeller)
    },

    onCheckBrand(checkedBrand) {
      if (this.checkedBrandsList.includes(checkedBrand))
        this.checkedBrandsList = this.checkedBrandsList.filter((brand) => brand !== checkedBrand)
      else this.checkedBrandsList.push(checkedBrand)
    },
  },
}
</script>

<style lang="scss" scoped>
.products-manager {
  display: flex;
  gap: 0 1.25rem;
}
</style>
