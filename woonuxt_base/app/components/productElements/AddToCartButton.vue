<script setup>
const { cart } = useCart();
const props = defineProps({
  disabled: { type: Boolean, default: false },
  size: { type: String, default: 'md' },
});
const isLoading = ref(false);
const { t } = useI18n();
const addToCartButtonText = computed(() => (isLoading.value ? t('messages.shop.adding') : t('messages.shop.addToCart')));

// stop loading when cart is updated
watch(cart, (val) => {
  isLoading.value = false;
});
</script>

<template>
  <!-- Egyetlen gyökér div elem, ami örökli a class attribútumokat -->
  <div>
    <button
      v-if="size === 'md'"
      type="submit"
      class="w-full bg-[#FF5D19] hover:bg-[#E54A0F] disabled:bg-gray-400 disabled:cursor-not-allowed text-white font-bold py-3 px-6 rounded-md transition-colors duration-200 flex items-center justify-center gap-2"
      :disabled="disabled"
      @click="isLoading = true">
      <span>{{ addToCartButtonText }}</span>
      <LoadingIcon v-if="isLoading" stroke="4" size="12" color="#fff" />
    </button>

    <PhosphorIconPlusCircle
      v-if="size === 'sm' && !isLoading"
      type="submit"
      class="w-[48px] h-[48px] hover:text-[#FF5D19] cursor-pointer transition rounded-lg flex font-bold text-center gap-4 items-center justify-center focus:outline-none"
      :class="{ 'opacity-50 cursor-not-allowed': disabled }"
      :disabled="disabled"
      @click="!disabled && (isLoading = true)"/>
    <LoadingIcon v-if="size === 'sm' && isLoading" stroke="4" size="46" color="#FF5D19" />
  </div>
</template>