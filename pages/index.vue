<script lang="ts" setup>
import {computed, ref} from 'vue';
  import Product from '../components/Product.vue';
  import { productList } from '~/ultils/example';
  import Header from '../components/Header.vue';
  import ProductModal from '../components/ProductModal.vue';

  export interface ProductType {
    id: string,
    name: string,
    title: string,
    des: string,
    price: number,
    image: string,
  }

  const productId = ref<string>('');
  const openModal = (id: string) => (productId.value = id);
  const closeModal = () => (productId.value = '');

  const item = computed(() => (productList.find((i: ProductType) => i.id === productId.value)))
</script>

<style>
  .container {
    @apply flex justify-center items-center justify-center m-2.5
  }
  .product-container {
    @apply w-full grid gap-4 grid-cols-3;
  }
</style>

<template>
  <div v-if="productId === ''">
    <Header />
    <div class="container" >
      <div class="product-container">
        <Product
          v-for="product in productList"
          :key="product.id"
          :item="product"
          @openModal="openModal"
        />
      </div>
    </div>
  </div>
  <ProductModal
    :item="item"
    :open="productId !== ''"
    @closeModal="closeModal"
  />
</template>
