<script setup>
const { toggleCart, cart } = useCart();
</script>

<template>
  <div class="relative cursor-pointer inline-flex items-center" title="Cart" @click="toggleCart">
    <svg 
      xmlns="http://www.w3.org/2000/svg" 
      width="22" 
      height="22" 
      viewBox="0 0 22 22" 
      fill="none"
      class="w-8 h-8"
    >
      <path d="M7.5625 19.9375C8.32189 19.9375 8.9375 19.3219 8.9375 18.5625C8.9375 17.8031 8.32189 17.1875 7.5625 17.1875C6.80311 17.1875 6.1875 17.8031 6.1875 18.5625C6.1875 19.3219 6.80311 19.9375 7.5625 19.9375Z" fill="#F3F3F3"/>
      <path d="M16.5 19.9375C17.2594 19.9375 17.875 19.3219 17.875 18.5625C17.875 17.8031 17.2594 17.1875 16.5 17.1875C15.7406 17.1875 15.125 17.8031 15.125 18.5625C15.125 19.3219 15.7406 19.9375 16.5 19.9375Z" fill="#F3F3F3"/>
      <path d="M1.375 2.75H3.4375L6.5957 14.1178C6.67608 14.4073 6.84907 14.6625 7.08823 14.8444C7.32738 15.0263 7.61954 15.1249 7.92 15.125H16.4141C16.7147 15.1251 17.007 15.0266 17.2464 14.8447C17.4857 14.6628 17.6588 14.4075 17.7392 14.1178L19.9375 6.1875H4.39227" stroke="#F3F3F3" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>

    <ClientOnly>
      <Transition name="popIn" mode="out-in">
        <span
          v-if="cart?.contents?.itemCount > 0"
          class="bg-primary rounded-full text-white leading-none min-w-[16px] p-[3px] -top-1 -right-1 md:-right-2 text-[10px] absolute inline-flex justify-center items-center">
          {{ cart?.contents?.itemCount }}
        </span>
      </Transition>
    </ClientOnly>
  </div>
</template>

<style lang="postcss">
/* popIn */
.popIn-enter-active,
.popIn-leave-active {
  transition: all 200ms cubic-bezier(0, 0, 0.57, 1.61);
}

.popIn-enter-from,
.popIn-leave-to {
  transform: scale(0);
}
</style>