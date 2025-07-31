<script setup lang="ts">
const footerLinks = [
  { name: 'Mi az a teqball?', link: '/teqball' },
  { name: 'Termékeink', link: '/products' },
  { name: 'Kapcsolat', link: '/contact' },
  { name: 'Kosaram', link: '/cart' },
  { name: 'Adatkezelési Nyilatkozat', link: '/privacy-policy' },
  { name: 'Hivatalos TeqBall oldal', link: 'https://teqball.com', external: true },
]
</script>

<template>
  <footer class="bg-white">
    <div class="container mx-auto px-4 py-8">
      <div class="flex flex-col md:flex-row justify-between items-center gap-8">
        
        <!-- Bal oldal: Logo -->
        <div class="flex-shrink-0">
          <NuxtLink to="/" class="block">
            <NuxtImg 
              src="/img/footer-logo.svg" 
              alt="G TEO SPORT" 
              class="h-5 w-auto"
            />
          </NuxtLink>
        </div>

        <!-- Középső rész: Navigációs linkek -->
        <nav class="flex flex-wrap justify-center items-center gap-6 md:gap-8">
          <NuxtLink 
            v-for="link in footerLinks" 
            :key="link.name"
            :to="link.link"
            :target="link.external ? '_blank' : '_self'"
            :rel="link.external ? 'noopener noreferrer' : ''"
            class="text-gray-600 hover:text-gray-900 transition-colors duration-200 text-sm md:text-base whitespace-nowrap"
          >
            {{ link.name }}
          </NuxtLink>
        </nav>

        <!-- Jobb oldal: Digital Seed Studio logo -->
        <div class="flex-shrink-0">
          <a 
            href="https://digitalseed.hu" 
            target="_blank" 
            rel="noopener noreferrer"
            class="block opacity-60 hover:opacity-100 transition-opacity duration-200"
            title="Digital Seed Studio"
          >
            <NuxtImg 
              src="/img/digitalseed.svg" 
              alt="Digital Seed Studio" 
              class="h-10 w-auto"
            />
          </a>
        </div>

      </div>
    </div>
  </footer>
</template>

<style scoped>
.container {
  max-width: 1200px;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  nav {
    order: 3;
    width: 100%;
  }
  
  .flex-shrink-0:last-child {
    order: 2;
  }
}
</style>