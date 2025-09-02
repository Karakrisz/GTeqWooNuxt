<script setup lang="ts">
import { ref, watch } from 'vue'

// Form state
const formData = ref({
  name: '',
  email: '',
  message: ''
})

const isSubmitting = ref(false)
const isSubmitted = ref(false)

// Form submission
const submitForm = async () => {
  if (!formData.value.name || !formData.value.email || !formData.value.message) {
    return
  }

  isSubmitting.value = true
  
  try {
    // Itt implementálhatod a form submission logikát
    // pl. API hívás, email küldés, stb.
    
    // Szimulált delay
    await new Promise(resolve => setTimeout(resolve, 1000))
    
    isSubmitted.value = true
    
    // Form reset
    formData.value = {
      name: '',
      email: '',
      message: ''
    }
    
  } catch (error) {
    console.error('Hiba a form küldéskor:', error)
  } finally {
    isSubmitting.value = false
  }
}

// Success message auto-hide
watch(isSubmitted, (newValue) => {
  if (newValue) {
    setTimeout(() => {
      isSubmitted.value = false
    }, 3000)
  }
})
</script>

<template>
  <section class="px-6 md:px-0">
    <div class="container bg-[#FF5D19] rounded-3xl p-8 md:p-20 mx-auto">
      <!-- Fejléc -->
      <div class="mb-8">
        <h2 class="text-white font-bold text-2xl uppercase leading-none mb-4">
          ÍRJON NEKÜNK E-MAILT
        </h2>
        <p class="text-white font-normal text-base leading-none max-w-4xl">
          Kérdése van, ajánlatot kérne, vagy csak többet szeretne megtudni a teqball asztalokról? Forduljon hozzánk bizalommal – örömmel segítünk! Várjuk levelét az alábbi e-mail címen, és igyekszünk mihamarabb válaszolni.
        </p>
      </div>

      <!-- Form -->
      <form @submit.prevent="submitForm" class="space-y-6">
        <!-- Név és Email egy sorban -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <!-- Név mező -->
          <div>
            <input
              v-model="formData.name"
              type="text"
              placeholder="Név*"
              required
              class="w-full px-6 py-4 bg-white rounded-md border-0 placeholder-[#C8C8C8] text-gray-800 font-normal text-base leading-none focus:outline-none focus:ring-2 focus:ring-white/30 transition-all"
            />
          </div>
          
          <!-- Email mező -->
          <div>
            <input
              v-model="formData.email"
              type="email"
              placeholder="E-mail cím*"
              required
              class="w-full px-6 py-4 bg-white rounded-md border-0 placeholder-[#C8C8C8] text-gray-800 font-normal text-base leading-none focus:outline-none focus:ring-2 focus:ring-white/30 transition-all"
            />
          </div>
        </div>

        <!-- Üzenet mező -->
        <div>
          <textarea
            v-model="formData.message"
            placeholder="Üzenet"
            rows="6"
            required
            class="w-full px-6 py-4 bg-white rounded-md border-0 placeholder-[#C8C8C8] text-gray-800 font-normal text-base leading-none focus:outline-none focus:ring-2 focus:ring-white/30 transition-all resize-none"
          ></textarea>
        </div>

        <!-- Alsó rész: Adatvédelem és gomb -->
        <div class="flex flex-col md:flex-row md:items-end md:justify-between gap-6 pt-4">
          <!-- Adatvédelmi nyilatkozat -->
          <div class="text-white font-normal text-base leading-none">
            A küldés gombra kattintva elfogadja az 
            <NuxtLink to="/" class="underline hover:text-white transition-colors">
              Adatvédelmi Nyilatkozatot
            </NuxtLink>
          </div>

          <!-- Küldés gomb -->
          <button
            type="submit"
            :disabled="isSubmitting || !formData.name || !formData.email || !formData.message"
            class="bg-[#242424] hover:bg-[#1a1a1a] disabled:bg-gray-600 disabled:cursor-not-allowed text-white font-semibold px-8 py-4 rounded-md transition-all duration-200 flex items-center gap-3 min-w-[140px] justify-center group"
          >
            <span v-if="!isSubmitting">Küldés</span>
            <span v-else>Küldés...</span>
            
            <!-- Küldés ikon -->
            <svg 
              v-if="!isSubmitting"
              xmlns="http://www.w3.org/2000/svg" 
              width="20" 
              height="20" 
              viewBox="0 0 20 20" 
              fill="none"
              class="w-5 h-5 group-hover:translate-x-1 transition-transform"
            >
              <path d="M8.4375 11.5625L12.5 7.5" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
              <path d="M17.4757 3.29526C17.5059 3.18834 17.5069 3.07533 17.4789 2.96786C17.4508 2.86039 17.3946 2.76233 17.3161 2.68379C17.2376 2.60525 17.1395 2.54906 17.032 2.521C16.9246 2.49294 16.8115 2.49403 16.7046 2.52416L1.70463 7.0726C1.58217 7.10716 1.47317 7.17828 1.39221 7.27645C1.31125 7.37461 1.26219 7.49516 1.25157 7.62196C1.24095 7.74876 1.26929 7.87578 1.3328 7.98605C1.39631 8.09631 1.49197 8.18456 1.60698 8.23901L8.43745 11.5624L11.7609 18.3921C11.8153 18.5071 11.9036 18.6028 12.0138 18.6663C12.1241 18.7298 12.2511 18.7582 12.3779 18.7475C12.5047 18.7369 12.6253 18.6879 12.7234 18.6069C12.8216 18.5259 12.8927 18.4169 12.9273 18.2945L17.4757 3.29526Z" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
            
            <!-- Loading spinner -->
            <div v-else class="w-5 h-5 border-2 border-white/30 border-t-white rounded-full animate-spin"></div>
          </button>
        </div>
      </form>

      <!-- Success message -->
      <div
        v-if="isSubmitted"
        class="mt-6 bg-white/20 backdrop-blur border border-white/30 rounded-xl p-4 text-white text-center"
      >
        <div class="flex items-center justify-center gap-2">
          <svg class="w-5 h-5 text-green-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
          </svg>
          <span>Köszönjük! Üzenetét sikeresen elküldtük.</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Custom focus styles */
input:focus,
textarea:focus {
  box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.1);
}

/* Loading animation */
@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.animate-spin {
  animation: spin 1s linear infinite;
}
</style>