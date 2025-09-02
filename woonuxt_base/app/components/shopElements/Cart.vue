<script setup lang="ts">
const { cart, toggleCart, isUpdatingCart } = useCart();
</script>

<template>
  <div class="fixed top-0 bottom-0 right-0 z-50 flex flex-col w-11/12 max-w-lg overflow-x-hidden bg-white shadow-lg">
    <EmptyCart v-if="cart && !cart.isEmpty" class="absolute top-6 md:left-8 left-6 rounded-md shadow-lg p-1.5 w-fit hover:bg-red-400 hover:text-white transition-colors" />

    <Icon name="ion:close-outline" class="absolute p-1 rounded-md shadow-lg top-6 right-6 md:right-8 cursor-pointer hover:text-[#FF5D19] transition-colors" size="34" @click="toggleCart(false)" />

    <div class="mt-8 text-center text-dark font-medium text-lg">
      {{ $t('messages.shop.cart') }}
      <span v-if="cart?.contents?.productCount" class="text-secondary"> ({{ cart?.contents?.productCount }}) </span>
    </div>

    <ClientOnly>
      <template v-if="cart && !cart.isEmpty">
        <ul class="flex flex-col flex-1 gap-4 p-6 overflow-y-scroll md:p-8">
          <CartCard v-for="item in cart.contents?.nodes" :key="item.key" :item />
        </ul>
        <div class="px-8 mb-8">
          <NuxtLink
            class="bg-[#FF5D19] hover:bg-[#E54A0F] text-white font-bold py-3 px-6 rounded-md transition-colors duration-200 flex items-center justify-between w-full"
            to="/checkout"
            @click.prevent="toggleCart()">
            <span class="mx-2">{{ $t('messages.shop.checkout') }}</span>
            <span v-html="cart.total" class="font-semibold" />
          </NuxtLink>
        </div>
      </template>
      <!-- Empty Cart Message -->
      <EmptyCartMessage v-else-if="cart && cart.isEmpty" />
      <!-- Cart Loading -->
      <div v-else class="flex flex-col items-center justify-center flex-1 mb-20">
        <LoadingIcon />
      </div>
    </ClientOnly>
    <!-- Cart Loading Overlay -->
    <div v-if="isUpdatingCart" class="absolute inset-0 flex items-center justify-center bg-white bg-opacity-75 backdrop-blur-sm">
      <LoadingIcon />
    </div>
  </div>
</template>