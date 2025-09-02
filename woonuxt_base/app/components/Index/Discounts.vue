<script setup>
// Use better composables for data fetching
const {
  data: saleProductsData,
  pending,
  error,
} = useLazyAsyncData(
  'sale-products',
  () =>
    useAsyncGql('getProducts', {
      first: 5,
      orderby: 'POPULARITY',
      where: {
        onSale: true,
      },
    }).then(({ data }) => data.value?.products?.nodes || []),
  {
    default: () => [],
    immediate: true,
    watch: false,
  },
);

watchEffect(() => {
  if (error.value) {
    console.error('Error fetching products:', error.value);
  }
});

const onSaleProducts = computed(() => saleProductsData.value);
</script>

<template>
  <section class="w-full py-[50px] px-6 md:px-0">
    <div class="container product-content">
      <h2 class="text-[#242424] font-black text-[32px] uppercase leading-none mb-10">ASZTALAINK</h2>

      <TransitionGroup v-if="pending" name="fade" tag="div" class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-[24px] pb-[35px]">
        <div v-for="i in 3" :key="i" class="animate-pulse">
          <div class="bg-stone-200 h-48 rounded-lg mb-4" />
          <div class="space-y-3">
            <div class="h-4 bg-stone-200 rounded w-3/4" />
            <div class="h-4 bg-stone-200 rounded w-1/2" />
            <div class="h-4 bg-stone-200 rounded w-1/4" />
          </div>
        </div>
      </TransitionGroup>

      <template v-else>
        <div v-if="error" class="text-center text-red-600 pb-[35px]">Failed to load products. Please try again later.</div>
        <ProductRow v-else :products="onSaleProducts" class="pb-[35px]" />
      </template>

      <div class="flex gap-[10px] items-center justify-start">
        <NuxtLink to="/products" class="text-[#242424] hover:text-[#FF5D19] transition-colors"> Tovább az összes termékhez </NuxtLink>
        <PhosphorIconArrowRight class="text-[#FF5D19]" />
      </div>
    </div>
  </section>
</template>