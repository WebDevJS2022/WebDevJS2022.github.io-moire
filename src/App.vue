<template>
  <main class="content container">
    <div class="content__top">

      <div class="content__row">
        <h1 class="content__title">
          Каталог
        </h1>
        <span class="content__info">
          152 товара
        </span>
      </div>
    </div>

    <div class="content__catalog">
      <ProductFilter v-model:price-from="filterPriceFrom"
      v-model:price-to="filterPriceTo"
      v-model:category-id="filterCategoryId"/>

      <section class="catalog">
        <ProductList :products="products" />
        <BasePagination :modelValue="page" @update:modelValue="page = $event" :count="countProducts"
          :per-page="productsPerPage" />
      </section>

    </div>
  </main>
</template>

<script>
import ProductList from '@/components/ProductList.vue';
import products from '@/data/products';
import BasePagination from '@/components/BasePagination.vue';
import ProductFilter from './components/ProductFilter.vue';

export default {
  name: 'App',
  data() {
    return {
      filterPriceFrom: 0,
      filterPriceTo: 0,
      filterCategoryId: 0,

      page: 1,
      productsPerPage: 3,
    };
  },
  computed: {
    // вычисляемое свойство, кот будет возвращать отфильтрованный список товаров
    filteredProducts() {
      let filteredProducts = products;

      if (this.filterPriceFrom > 0) {
        filteredProducts = filteredProducts
          .filter((product) => product.price > this.filterPriceFrom);
      }
      if (this.filterPriceTo > 0) {
        filteredProducts = filteredProducts
          .filter((product) => product.price < this.filterPriceTo);
      }
      if (this.filterCategoryId) {
        filteredProducts = filteredProducts
          .filter((product) => product.categoryId === this.filterCategoryId);
      }
      return filteredProducts;
    },

    products() {
      const offset = (this.page - 1) * this.productsPerPage;
      return this.filteredProducts.slice(offset, offset + this.productsPerPage);
    },
    countProducts() {
      return this.filteredProducts.length;
    },
  },
  components: { ProductList, BasePagination, ProductFilter },
};
</script>
