<script setup lang="ts">
import { Head, Link } from '@inertiajs/vue3';
import { ref, onMounted, onUnmounted } from 'vue';
import { Icon } from '@iconify/vue';

const isMenuOpen = ref(false);
const isSubMenuOpen = ref(false);
const isLoginPopupOpen = ref(false);
const isScrolled = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
  if (isMenuOpen.value) {
    document.body.style.overflow = 'hidden';
  } else {
    document.body.style.overflow = '';
  }
};

const toggleSubMenu = () => {
  isSubMenuOpen.value = !isSubMenuOpen.value;
};

const toggleLoginPopup = () => {
  isLoginPopupOpen.value = !isLoginPopupOpen.value;
};

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  document.body.style.overflow = '';
});
</script>

<template>
  <Head title="Cari, Bayar, & Sewa Kost Impianmu Secara Online">
    <link rel="preconnect" href="https://rsms.me/" />
    <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
  </Head>

  <!-- Header for Desktop -->
  <header class="bg-slate-950 sticky top-0 z-50 shadow-md hidden md:block">
    <div class="container mx-auto px-4">
      <div class="flex justify-between items-center py-4">
        <div class="flex items-center space-x-4">
          <h1 class="text-2xl font-bold" style="font-family: 'VT323', monospace;">
            <Link :href="route('home')">
              <span class="text-white">PKUKOS</span>
            </Link>
          </h1>
          
          <!-- Desktop Search Bar (shown when scrolled) -->
          <transition
            enter-active-class="transition-all duration-300 ease-out"
            enter-from-class="opacity-0 -translate-x-4"
            enter-to-class="opacity-100 translate-x-0"
            leave-active-class="transition-all duration-200 ease-in"
            leave-from-class="opacity-100 translate-x-0"
            leave-to-class="opacity-0 -translate-x-4"
          >
            <div v-if="isScrolled" class="relative">
              <input 
                type="text" 
                placeholder="Masukan nama lokasi/area/alamat" 
                class="w-86 bg-slate-800 text-white rounded-lg py-2 pl-10 pr-4 focus:outline-none focus:ring-2 focus:ring-teal-500"
              >
              <Icon 
                icon="pixelarticons:search" 
                class="absolute left-3 top-2.5 text-slate-400 w-5 h-5"
              />
            </div>
          </transition>
        </div>
        
        <!-- Desktop Navigation -->
        <nav>
          <ul class="flex space-x-6 items-center">
            <li @click="toggleSubMenu" class="relative text-white hover:text-slate-200 transition-colors duration-200 font-medium">
              Cari Apa?
              <svg class="inline-block w-4 h-4 ml-1 transition-transform duration-200" :class="{'rotate-180': isSubMenuOpen}" fill="currentColor" viewBox="0 0 20 20">
                <path d="M5.23 7.21a.75.75 0 011.06 0L10 10.44l3.71-3.23a.75.75 0 111.06 1.06l-4.25 3.5a.75.75 0 01-1.06 0l-4.25-3.5a.75.75 0 010-1.06z" />
              </svg>
              <ul v-show="isSubMenuOpen" class="absolute left-0 mt-2 bg-white shadow-lg rounded-md overflow-hidden">
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
            <li class="relative">
              <button 
                @click="toggleLoginPopup"
                class="button" 
                style="width: 100px;"
              >
                <span>Masuk</span>
              </button>
              
              <!-- Login Popup -->
              <transition
                enter-active-class="transition-all duration-200 ease-out"
                enter-from-class="opacity-0 translate-y-2"
                enter-to-class="opacity-100 translate-y-0"
                leave-active-class="transition-all duration-150 ease-in"
                leave-from-class="opacity-100 translate-y-0"
                leave-to-class="opacity-0 translate-y-2"
              >
                <div 
                  v-if="isLoginPopupOpen" 
                  class="absolute right-0 mt-2 w-64 bg-slate-800 rounded-lg shadow-xl border border-slate-700 overflow-hidden z-50"
                >
                  <div class="p-4">
                    <h3 class="text-white font-medium text-center mb-3">Masuk Sebagai</h3>
                    <div class="space-y-2">
                      <Link 
                        href="/login" 
                        class="block w-full text-center button py-2 px-4"
                        @click="toggleLoginPopup"
                      >
                        <span>Pemilik</span>
                      </Link>
                      <Link 
                        href="/login/pencari" 
                        class="block w-full text-center button pencari-button py-2 px-4"
                        @click="toggleLoginPopup"
                      >
                        <span>Pencari</span>
                      </Link>
                    </div>
                  </div>
                </div>
              </transition>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </header>

  <!-- Header for Mobile -->
  <header class="bg-slate-950 sticky top-0 z-50 shadow-md md:hidden">
    <!-- Normal Header (shown when not scrolled) -->
    <transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-4"
    >
      <div v-if="!isScrolled" class="container mx-auto px-4">
        <div class="flex justify-between items-center py-4">
          <h1 class="text-2xl font-bold" style="font-family: 'VT323', monospace;">
            <Link :href="route('home')">
              <span class="text-white">PKUKOS</span>
            </Link>
          </h1>
          
          <button 
            @click="toggleMenu"
            class="text-white focus:outline-none focus:ring-2 focus:ring-white rounded-lg p-1"
            aria-label="Toggle menu"
          >
            <Icon 
              :icon="isMenuOpen ? 'pixelarticons:close' : 'pixelarticons:menu'"
              class="w-6 h-6"
            />
          </button>
        </div>
      </div>
    </transition>

    <!-- Mobile Search Bar (shown when scrolled) -->
    <transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-4"
    >
      <div v-if="isScrolled" class="bg-slate-900 py-3 px-4">
        <div class="relative">
          <input 
            type="text" 
            placeholder="Mau ngekos di mana?" 
            class="w-full bg-slate-800 text-white rounded-lg py-2 pl-10 pr-4 focus:outline-none focus:ring-2 focus:ring-teal-500"
          >
          <Icon 
            icon="pixelarticons:search" 
            class="absolute left-3 top-2.5 text-slate-400 w-5 h-5"
          />
        </div>
      </div>
    </transition>

    <!-- Full Screen Mobile Navigation -->
    <transition
    enter-active-class="transition-all duration-300 ease-out"
    enter-from-class="opacity-0 translate-x-full"
    enter-to-class="opacity-100 translate-x-0"
    leave-active-class="transition-all duration-200 ease-in"
    leave-from-class="opacity-100 translate-x-0"
    leave-to-class="opacity-0 translate-x-full"
  >
    <div v-if="isMenuOpen" class="fixed inset-0 z-50 bg-slate-950 overflow-y-auto">
      <div class="absolute inset-y-0 right-0 w-full max-w-sm bg-slate-950 border-l border-slate-800 overflow-y-auto">
        <div class="container mx-auto px-4 pt-4">
          <div class="flex justify-between items-center pb-4 border-b border-slate-800">
            <h1 class="text-2xl font-bold" style="font-family: 'VT323', monospace;">
              <span class="text-white">PKUKOS</span>
            </h1>
            <button 
              @click="toggleMenu"
              class="text-white focus:outline-none focus:ring-2 focus:ring-white rounded-lg p-1"
              aria-label="Close menu"
            >
              <Icon 
                icon="pixelarticons:close"
                class="w-6 h-6"
              />
            </button>
          </div>

          <nav class="py-4">
            <ul class="flex flex-col space-y-4">
              <div class="border-b border-slate-800 pb-4">
                <li v-for="item in navItemsul" :key="item.name">
                  <Link 
                    :href="item.href"
                    class="flex items-center gap-4 min-h-[48px] text-white font-medium py-2 px-3 
                          hover:bg-slate-800 hover:text-slate-100 transition-colors duration-200 rounded-lg"
                    @click="toggleMenu"
                  >
                    <Icon 
                      v-if="item.icon"
                      :icon="item.icon" 
                      class="w-5 h-5 flex-shrink-0"
                    />
                    <span class="text-lg">{{ item.name }}</span>
                    <Icon 
                      icon="pixelarticons:chevron-right" 
                      class="w-5 h-5 ml-auto text-slate-400 group-hover:text-white"
                    />
                  </Link>
                </li>
              </div>
              <div class="border-b border-slate-800 pb-4">
                <li v-for="item in navItemsMobile" :key="item.name">
                  <Link 
                    :href="item.href" 
                    class="block text-white hover:text-slate-200 transition-colors duration-200 py-3 px-3 rounded-lg hover:bg-slate-800 text-lg"
                    @click="toggleMenu"
                  >
                    {{ item.name }}
                  </Link>
                </li>
              </div>
              <li class="pt-2">
                <Link href="/login/pemilik" class="button w-full py-3 text-lg block text-center" @click="toggleMenu">
                  <span>Masuk Sebagai Pemilik</span>
                </Link>
              </li>
              <li>
                <Link href="/login/pencari" class="button pencari-button w-full py-3 text-lg block text-center" @click="toggleMenu">
                  <span>Masuk Sebagai Pencari</span>
                </Link>
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </div>
  </transition>
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
  padding: 8px 10px;
  border-radius: 10px;
  font-size: 1em;
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
  background: rgb(30 41 59);
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
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: transparent;
}

/* Close popup when clicking outside */
.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  z-index: 40;
}
</style>