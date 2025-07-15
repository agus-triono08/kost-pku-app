<script setup lang="ts">
import { Head, Link } from '@inertiajs/vue3';
import { ref } from 'vue';
import { Icon } from '@iconify/vue'

const isMenuOpen = ref(false);
const isSubMenuOpen = ref(false);
const isLoginPopupOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const toggleSubMenu = () => {
  isSubMenuOpen.value = !isSubMenuOpen.value;
};

const toggleLoginPopup = () => {
  isLoginPopupOpen.value = !isLoginPopupOpen.value;
};
</script>

<template>
  <Head title="Cari, Bayar, & Sewa Kost Impianmu Secara Online">
    <link rel="preconnect" href="https://rsms.me/" />
    <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
  </Head>

  <header class="bg-slate-950 sticky top-0 z-50 shadow-md">
    <div class="container mx-auto px-4">
      <div class="flex justify-between items-center py-4">
        <h1 class="text-2xl font-bold" style="font-family: 'VT323', monospace;">
          <Link :href="route('home')">
            <span class="text-white">KOST</span>
            <span class="text-teal-400">PKU</span>
          </Link>
        </h1>
        
        <!-- Desktop Navigation -->
        <nav class="hidden md:block">
          <ul class="flex space-x-6">
            <li @click="toggleSubMenu" class="relative text-white hover:text-slate-200 transition-colors duration-200 font-medium">
              Cari Apa?
              <svg class="inline-block w-4 h-4 ml-1 transition-transform duration-200" :class="{'rotate-180': isSubMenuOpen}" fill="currentColor" viewBox="0 0 20 20">
                <path d="M5.23 7.21a.75.75 0 011.06 0L10 10.44l3.71-3.23a.75.75 0 111.06 1.06l-4.25 3.5a.75.75 0 01-1.06 0l-4.25-3.5a.75.75 0 010-1.06z" />
              </svg>
              <ul v-show="isSubMenuOpen" class="absolute left-0 mt-2 bg-white shadow-lg">
                <li v-for="item in navItemsul" :key="item.name">
                  <Link
                    :href="item.href"
                    class="flex items-center gap-2 min-h-[40px] text-slate-700 font-medium py-2 px-3 
                          hover:bg-slate-100 hover:text-slate-800 transition-colors duration-200"
                  >
                    <Icon 
                      v-if="item.icon"
                      :icon="item.icon" 
                      class="w-6 h-6 flex-shrink-0"
                    />
                    {{ item.name }}
                  </Link>
                </li>                
              </ul>
            </li>
            <li v-for="item in navItems" :key="item.name">
              <Link 
                :href="item.href" 
                class="text-white hover:text-slate-200 transition-colors duration-200 font-medium"
              >
                {{ item.name }}
              </Link>
            </li>
            <li class="flex-grow">
              <button class="button" style="width: 100px;">
                <span>Masuk</span>
              </button>
            </li>
          </ul>
        </nav>
        
        <!-- Mobile Toggle Button -->
        <button 
          @click="toggleMenu"
          class="md:hidden text-white focus:outline-none focus:ring-2 focus:ring-white rounded-lg p-1"
          aria-label="Toggle menu"
        >
          <!-- Gunakan ikon dari Pixelarticons -->
          <Icon 
            :icon="isMenuOpen ? 'pixelarticons:close' : 'pixelarticons:menu'"
            class="w-6 h-6"
          />
        </button>
      </div>
      
      <!-- Mobile Navigation -->
      <transition
        enter-active-class="transition-all duration-300 ease-out"
        enter-from-class="opacity-0 translate-x-full"
        enter-to-class="opacity-100 translate-x-0"
        leave-active-class="transition-all duration-200 ease-in"
        leave-from-class="opacity-100 translate-x-0"
        leave-to-class="opacity-0 translate-x-full"
      >
        <nav v-show="isMenuOpen" class="md:hidden pb-4">
          <ul class="flex flex-col space-y-3">
            <div class="border-b border-slate-100 border-opacity-100">
              <li v-for="item in navItemsul" :key="item.name">
                <Link 
                  :href="item.href"
                  class="flex items-center gap-2 min-h-[40px] text-white font-medium py-2 px-3 
                        hover:bg-slate-700 hover:text-slate-100 transition-colors duration-200"
                >
                  <!-- Icon di kiri -->
                  <Icon 
                    v-if="item.icon"
                    :icon="item.icon" 
                    class="w-4 h-4 flex-shrink-0"
                  />
                  
                  <!-- Teks -->
                  {{ item.name }}
                  
                  <!-- Chevron Right di kanan -->
                  <Icon 
                    icon="pixelarticons:chevron-right" 
                    class="w-4 h-4 ml-auto text-slate-400 group-hover:text-white"
                  />
                </Link>
              </li>
            </div>
            <div class="border-b border-slate-100 border-opacity-100">
              <li v-for="item in navItemsMobile" :key="item.name">
                <Link 
                  :href="item.href" 
                  class="block text-white hover:text-slate-200 transition-colors duration-200 py-2 px-3 rounded hover:bg-slate-600"
                  @click="toggleMenu"
                >
                  {{ item.name }}
                </Link>
              </li>
            </div>
            <li class="flex justify-center">
              <button class="button" style="width: 100%;">
                <span>Masuk Sebagai Pemilik</span>
              </button>
            </li>
            <li class="flex justify-center">
              <button class="button pencari-button" style="width: 100%;">
                <span>Masuk Sebagai Pencari</span>
              </button>
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
        { name: 'Pusat Bantuan', href: '#' },
        { name: 'Syarat dan Ketentuan', href: '#' },
      ],
      navItemsMobile: [
        { name: 'Pusat Bantuan', href: '#' },
        { name: 'Blog Kost PKU', href: '#' },
        { name: 'Syarat dan Ketentuan', href: '#' },
        { name: 'Kebijakan Privasi', href: '#' },
      ],
      navItemsul: [
        {name: 'Kost', href: '#', icon: 'pixelarticons:bed'},
        {name: 'Kontrakan', href: '#', icon: 'pixelarticons:building-community'},
        {name: 'Ruko', href: '#', icon: 'pixelarticons:store'},
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

  .button {
    position: relative;
    text-decoration: none;
    color: #fff;
    background: linear-gradient(45deg, #0ce39a, #69007f, #fc0987);
    padding: 8px 10px; /* Ubah padding sesuai kebutuhan */
    border-radius: 10px;
    font-size: 1em; /* Ubah ukuran font sesuai kebutuhan */
    font-family: 'VT323', monospace;
    cursor: pointer;
    height: 100%;    
  }

  .button span {
    position: relative;
    z-index: 1;
  }

  .button::before {
    content: "";
    position: absolute;
    inset: 1px;
    background: rgb(2 6 23);
    border-radius: 9px;
    transition: 0.5s;
  }

  .pencari-button::before {
    background: rgb(30 41 59); /* Ganti dengan warna yang diinginkan */
  }

  .button:hover::before {
    opacity: 0.7;
  }

  .button::after {
    content: "";
    position: absolute;
    inset: 0px;
    background: linear-gradient(45deg, #0ce39a, #69007f, #fc0987);
    border-radius: 9px;
    transition: 0.5s;
    opacity: 0;
    filter: blur(20px);
  }

  .button:hover:after {
    opacity: 1;
  }

  .gradient-text {
    background: linear-gradient(45deg, #0ce39a, #69007f, #fc0987);
    -webkit-background-clip: text; /* For WebKit-based browsers */
    background-clip: text; /* Standard property */
    -webkit-text-fill-color: transparent; /* For WebKit-based browsers */
    color: transparent; /* Fallback for other browsers */
  }
</style>