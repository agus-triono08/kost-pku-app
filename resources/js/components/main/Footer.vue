<script setup lang="ts">
  import { ref } from 'vue';
  import { Icon } from '@iconify/vue';

  // Tahun otomatis
  const currentYear = new Date().getFullYear();

  const activeAccordion = ref<number | null>(null);

  const toggleAccordion = (index: number) => {
    activeAccordion.value = activeAccordion.value === index ? null : index;
  };

  interface MobileSection {
    title: string;
    items: {
      text: string;
      link: string;
    }[];
  }

  const mobileSections = ref<MobileSection[]>([
    {
      title: 'Tautan Cepat',
      items: [
        { text: 'Tentang Kami', link: '#' },
        { text: 'Cara Kerja', link: '#' },
        { text: 'Blog', link: '#' }
      ]
    },
    {
      title: 'Untuk Penyewa',
      items: [
        { text: 'Cari Kost', link: '#' },
        { text: 'Favorit Saya', link: '#' },
        { text: 'Riwayat', link: '#' },
        { text: 'Pusat Bantuan', link: '#' }
      ]
    },
    {
      title: 'Untuk Pemilik',
      items: [
        { text: 'Daftarkan Kost', link: '#' },
        { text: 'Kelola Kost', link: '#' },
        { text: 'Statistik', link: '#' },
        { text: 'Panduan Pemilik', link: '#' }
      ]
    }
  ]);
</script>
<template>
  <!-- Footer Section -->
  <footer class="bg-slate-950 text-slate-300 border-t border-slate-400">
    <div class="container mx-auto px-4 py-8">
      <!-- Grid Layout for Desktop -->
      <div class="hidden md:grid md:grid-cols-4 lg:grid-cols-5 gap-8">
        <!-- Logo and Description -->
        <div class="col-span-2 lg:col-span-1">
          <h2 class="text-2xl font-bold mb-4" style="font-family: 'VT323', monospace;">
            <span class="text-white">PKUKOS</span>
          </h2>
          <p class="text-sm mb-4">
            Dapatkan "info kost murah" hanya di PKUKOS.<br>Mau "Sewa Kost Murah"?
          </p>
          <div class="flex space-x-4">
            <a href="#" aria-label="Facebook" class="text-slate-400 hover:text-white transition-colors">
              <Icon icon="ri:facebook-fill" class="w-5 h-5" />
            </a>
            <a href="#" aria-label="Twitter" class="text-slate-400 hover:text-white transition-colors">
              <Icon icon="ri:twitter-x-fill" class="w-5 h-5" />
            </a>
            <a href="#" aria-label="Instagram" class="text-slate-400 hover:text-white transition-colors">
              <Icon icon="ri:instagram-fill" class="w-5 h-5" />
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div>
          <h3 class="text-white font-semibold mb-4 text-lg">Tautan Cepat</h3>
          <ul class="space-y-2">
            <li><a href="#" class="hover:text-white transition-colors">Tentang Kami</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Cara Kerja</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Blog</a></li>
          </ul>
        </div>

        <!-- For Tenants -->
        <div>
          <h3 class="text-white font-semibold mb-4 text-lg">Untuk Penyewa</h3>
          <ul class="space-y-2">
            <li><a href="#" class="hover:text-white transition-colors">Cari Kost</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Favorit Saya</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Riwayat</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Pusat Bantuan</a></li>
          </ul>
        </div>

        <!-- For Owners -->
        <div>
          <h3 class="text-white font-semibold mb-4 text-lg">Untuk Pemilik</h3>
          <ul class="space-y-2">
            <li><a href="#" class="hover:text-white transition-colors">Daftarkan Kost</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Kelola Kost</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Statistik</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Panduan Pemilik</a></li>
          </ul>
        </div>

        <!-- Contact -->
        <div class="lg:col-span-1">
          <h3 class="text-white font-semibold mb-4 text-lg">Kontak Kami</h3>
          <ul class="space-y-2">
            <li class="flex items-center">
              <Icon icon="pixelarticons:mail" class="w-5 h-5 mr-2" />
              <a href="mailto:cs@pkukos.com" class="hover:text-white transition-colors">cs@pkukos.com</a>
            </li>
            <li class="flex items-center">
              <Icon icon="pixelarticons:device-phone" class="w-5 h-5 mr-2" />
              <a href="tel:+628123456789" class="hover:text-white transition-colors">+62 812 3456 789</a>
            </li>
            <li class="flex items-center">
              <Icon icon="pixelarticons:map" class="w-5 h-5 mr-2" />
              <span>Pekanbaru, Indonesia</span>
            </li>
          </ul>
        </div>
      </div>

      <!-- Mobile Layout -->
      <div class="md:hidden">
        <!-- Accordion Menu -->
        <div class="space-y-4">
          <!-- Logo and Social -->
          <div class="mb-6">
            <h2 class="text-2xl font-bold mb-3" style="font-family: 'VT323', monospace;">
              <span class="text-white">PKUKOS</span>
            </h2>
            <p class="text-sm mb-4">
              Platform pencarian kost terbaik di Indonesia.
            </p>
            <div class="flex space-x-4">
              <a href="#" aria-label="Facebook" class="text-slate-400 hover:text-white transition-colors">
                <Icon icon="ri:facebook-fill" class="w-6 h-6" />
              </a>
              <a href="#" aria-label="Twitter" class="text-slate-400 hover:text-white transition-colors">
                <Icon icon="ri:twitter-x-fill" class="w-6 h-6" />
              </a>
              <a href="#" aria-label="Instagram" class="text-slate-400 hover:text-white transition-colors">
                <Icon icon="ri:instagram-fill" class="w-6 h-6" />
              </a>
            </div>
          </div>

          <!-- Accordion Items -->
          <div v-for="(section, index) in mobileSections" :key="index" class="border-b border-slate-800 pb-4">
            <button 
              @click="toggleAccordion(index)"
              class="flex justify-between items-center w-full text-left text-white font-semibold py-2"
            >
              <span>{{ section.title }}</span>
              <Icon 
                :icon="activeAccordion === index ? 'pixelarticons:chevron-up' : 'pixelarticons:chevron-down'" 
                class="w-5 h-5"
              />
            </button>
            <transition
              enter-active-class="transition-all duration-200 ease-out"
              enter-from-class="opacity-0 max-h-0"
              enter-to-class="opacity-100 max-h-96"
              leave-active-class="transition-all duration-150 ease-in"
              leave-from-class="opacity-100 max-h-96"
              leave-to-class="opacity-0 max-h-0"
            >
              <ul v-show="activeAccordion === index" class="pl-2 pt-2 space-y-2">
                <li v-for="(item, itemIndex) in section.items" :key="itemIndex">
                  <a :href="item.link" class="block py-1 hover:text-white transition-colors">{{ item.text }}</a>
                </li>
              </ul>
            </transition>
          </div>
        </div>

        <!-- Contact Info -->
        <div class="mt-6 pt-4 border-t border-slate-800">
          <h3 class="text-white font-semibold mb-3">Kontak Kami</h3>
          <ul class="space-y-2">
            <li class="flex items-center">
              <Icon icon="pixelarticons:mail" class="w-5 h-5 mr-2" />
              <a href="mailto:cs@pkukos.com" class="hover:text-white transition-colors">cs@pkukos.com</a>
            </li>
            <li class="flex items-center">
              <Icon icon="pixelarticons:device-phone" class="w-5 h-5 mr-2" />
              <a href="tel:+628123456789" class="hover:text-white transition-colors">+62 812 3456 789</a>
            </li>
          </ul>
        </div>
      </div>

      <!-- Copyright -->
      <div class="border-t border-slate-800 mt-8 pt-6 text-center text-sm text-slate-500">
        <p>© {{ currentYear }} PKUKOS. All rights reserved.</p>
        <div class="mt-2 flex justify-center space-x-4">
          <a href="#" class="hover:text-slate-300 transition-colors">Kebijakan Privasi</a>
          <a href="#" class="hover:text-slate-300 transition-colors">Syarat & Ketentuan</a>
        </div>
      </div>
    </div>
  </footer>
</template>
<style scoped>
/* Smooth transition for accordion */
.accordion-content {
  transition: max-height 0.3s ease, opacity 0.2s ease;
}
</style>