<script lang="ts" setup>
import {computed, PropType} from 'vue';
import { ProductType } from '~/pages/index.vue';
import { formatPrice } from '~/ultils/ultils-fn';

  const props = defineProps({
    item: Object as PropType<ProductType>,
    open: Boolean,
  })
  const emit = defineEmits(['closeModal'])
  const handleClose = () => (emit('closeModal'))

  const newPrice = computed(() => formatPrice(props.item.price))
</script>

<style>
  .bg-smoke-light {
    background-color: rgba(0, 0, 0, 0.4);
  }
  .modal-container {
    @apply fixed z-50 bg-smoke-light flex justify-center items-center h-full w-full
  }
  .modal {
    @apply relative bg-white w-1/3 rounded shadow
  }
  .image {
    background: linear-gradient(45deg, #0136af, #22abfa);
    @apply w-full
  }
  .nike {
    @apply top-0.5 uppercase absolute font-mono text-white text-9xl opacity-10 left-5 leading-relaxed
  }
  .modal-action {
    @apply bg-gray-200 rounded-b px-8 py-4 mt-8 flex justify-between items-center
  }
  .price {
    @apply text-4xl
  }
  .add-button {
    @apply text-white bg-blue-700 px-8 py-2 hover:bg-blue-900 rounded-lg mr-2
  }
  .close-button {
    @apply bg-white border border-gray-400 px-8 py-2 rounded-lg hover:bg-gray-500 hover:text-white
  }
</style>

<template>
  <div v-if="open" class="modal-container">
    <div class="modal">
      <div class="image">
        <img :src="item.image" :alt="item.image" />
        <h1 class="nike">nike</h1>
      </div>
      <p class="px-8 font-bold text-xl my-4">{{ item.name }} - {{ item.title }}</p>
      <div class="px-8 text-justify">
        <p class="text-xl">Product info</p>
        <p>{{ item.des }}</p>
      </div>
      <div class="modal-action">
        <span class="price">{{ newPrice }}</span>
        <div>
          <button class="add-button">Add to card</button>
          <button class="close-button" @click="handleClose">
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>