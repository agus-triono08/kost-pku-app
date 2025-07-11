<script setup lang="ts">
import { Head, Link } from '@inertiajs/vue3';
import { ref } from 'vue';

const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};
</script>

<template>
  <Head title="Cari, Bayar, & Sewa Kost Impianmu Secara Online">
    <link rel="preconnect" href="https://rsms.me/" />
    <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
  </Head>

  <header class="bg-teal-700 sticky top-0 z-50 shadow-md">
    <div class="container mx-auto px-4">
      <div class="flex justify-between items-center py-4">
        <h1 class="text-white text-2xl font-bold">KOST PKU</h1>
        
        <!-- Desktop Navigation -->
        <nav class="hidden md:block">
          <ul class="flex space-x-6">
            <li v-for="item in navItems" :key="item.name">
              <Link 
                :href="item.href" 
                class="text-white hover:text-teal-200 transition-colors duration-200 font-medium"
              >
                {{ item.name }}
              </Link>
            </li>
          </ul>
        </nav>
        
        <!-- Mobile Toggle Button -->
        <button 
          @click="toggleMenu"
          class="md:hidden text-white focus:outline-none focus:ring-2 focus:ring-white rounded-lg p-1"
          aria-label="Toggle menu"
        >
          <svg 
            class="w-6 h-6" 
            fill="none" 
            stroke="currentColor" 
            viewBox="0 0 24 24"
          >
            <path 
              stroke-linecap="round" 
              stroke-linejoin="round" 
              stroke-width="2" 
              :d="isMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'"
            />
          </svg>
        </button>
      </div>
      
      <!-- Mobile Navigation -->
      <transition
        enter-active-class="transition-all duration-300 ease-out"
        enter-from-class="opacity-0 -translate-y-4"
        enter-to-class="opacity-100 translate-y-0"
        leave-active-class="transition-all duration-200 ease-in"
        leave-from-class="opacity-100 translate-y-0"
        leave-to-class="opacity-0 -translate-y-4"
      >
        <nav v-show="isMenuOpen" class="md:hidden pb-4">
          <ul class="flex flex-col space-y-3">
            <li v-for="item in navItems" :key="item.name">
              <Link 
                :href="item.href" 
                class="block text-white hover:text-teal-200 transition-colors duration-200 py-2 px-3 rounded hover:bg-teal-600"
                @click="toggleMenu"
              >
                {{ item.name }}
              </Link>
            </li>
          </ul>
        </nav>
      </transition>
    </div>
  </header>
</template>

<script lang="ts">
export default {
  data() {
    return {
      navItems: [
        { name: 'Home', href: '#' },
        { name: 'About', href: '#' },
        { name: 'Services', href: '#' },
        { name: 'Contact', href: '#' }
      ]
    }
  }
}
</script>

<style scoped>
/* Animasi underline pada hover */
nav ul li a::after {
  content: '';
  display: block;
  width: 0;
  height: 2px;
  background: #99f6e4;
  transition: width 0.3s;
}

nav ul li a:hover::after {
  width: 100%;
}

@media (min-width: 768px) {
  nav ul li a::after {
    margin-top: 2px;
  }
}
</style>