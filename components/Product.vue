<script lang="ts" setup>
import { ProductType } from '~/pages/index.vue';
import { computed, PropType } from 'vue';
import { formatPrice } from '~/ultils/ultils-fn';

  const props = defineProps({
    item: Object as PropType<ProductType>
  })
  const emit = defineEmits(['openModal'])
  const handleClick = (id: string) => (emit('openModal', id))

  const newPrice = computed(() => formatPrice(props.item.price))

</script>

<style scoped>
  .container {
    @apply flex flex-col items-start p-2 shadow-xl cursor-pointer hover:shadow-2xl;
  }
  .name-container {
    @apply p-2.5;
  }
  .name {
    @apply text-4xl mr-2.5 pb-0.5;
  }
  .tag-name {
    @apply bg-blue-500 text-white rounded pt-0.5 pb-0.5 pl-2.5 pr-2.5 uppercase;
  }
  .price {
    @apply pl-2.5 text-2xl;
  }
</style>

<template>
  <div class="container" @click="handleClick(item.id)">
    <img :src="item.image" :alt="item.image" />
    <div>
      <div class="name-container">
        <h1 class="name">{{ item.name }}</h1>
        <span class="tag-name">New</span>
      </div>
      <div class="price">
        <span>{{ newPrice }}</span>
      </div>
    </div>
  </div>
</template>
