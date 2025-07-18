<script setup lang="ts">
  import { Link } from '@inertiajs/vue3';
  import { ref, computed } from 'vue';
  import { Icon } from '@iconify/vue';
  // Import Swiper
  import { Swiper, SwiperSlide } from 'swiper/vue';
  import { Autoplay, Pagination, Navigation } from 'swiper/modules';
  import type { Swiper as SwiperClass } from 'swiper';

  // Import Swiper styles
  import 'swiper/css';
  import 'swiper/css/pagination';

  const searchQuery = ref('')

  const handleSearch = () => {
    alert(`Mencari kost di: ${searchQuery.value}`)
  }

  // Sample data for cards
  const promoCards = ref([
    {
      id: 1,
      title: "Daftarkan Kos Anda di PKUKOS",
      description: "Berbagai fitur dan layanan untuk meningkatkan bisnis kos Anda.",
      image: "/storage/images/ilustrasi.png"
    }
  ])


  // Swiper modules
  const modules = [Navigation, Autoplay, Pagination]

  // Dummy data
  const kosList = [
    {
      id: 1,
      nama: "Kos Putri Anggrek",
      lokasi: "Tampan",
      harga: "Rp 750.000 / bulan",
      gambar: "https://images.unsplash.com/photo-1560448204-e02f11c3d0e2?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
      gender: "putri",
      fasilitas: ["Kamar mandi dalam", "Kipas", "Dapur bersama", "WiFi"],
      sisa_kamar: 2,
    },
    {
      id: 2,
      nama: "Kos Harapan Indah",
      lokasi: "Pekanbaru Kota",
      harga: "Rp 1.200.000 / bulan",
      gambar: "https://images.unsplash.com/photo-1522708323590-d24dbb6b0267?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
      gender: "campur",
      fasilitas: ["Kamar mandi dalam", "AC", "Laundry", "Parkir motor", "WiFi", "Dapur bersama", "Parkir mobil"],
      sisa_kamar: 0,
    },
    {
      id: 3,
      nama: "Kos Exclusive Harmony",
      lokasi: "Marpoyan Damai",
      harga: "Rp 950.000 / bulan",
      gambar: "https://images.unsplash.com/photo-1512917774080-9991f1c4c750?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
      gender: "putra",
      fasilitas: ["AC", "TV", "Lemari", "WiFi", "Dapur"],
      sisa_kamar: 2,
    },
    {
      id: 4,
      nama: "Kos Mahasiswa Ceria",
      lokasi: "Sukajadi",
      harga: "Rp 650.000 / bulan",
      gambar: "https://images.unsplash.com/photo-1580587771525-78b9dba3b914?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60",
      gender: "campur",
      fasilitas: ["Kipas", "Kamar mandi dalam", "Parkir motor"],
      sisa_kamar: 4,
    }
  ]

  const selectedLokasi = ref('')
  const swiperRef = ref<SwiperClass | null>(null)

  const onSwiperInit = (swiper: SwiperClass) => {
    swiperRef.value = swiper
  }


  const lokasiUnik = computed(() => {
    return [...new Set(kosList.map(item => item.lokasi))]
  })

  const filteredKos = computed(() => {
    if (!selectedLokasi.value) return kosList
    return kosList.filter(k => k.lokasi === selectedLokasi.value)
  })

  // Data untuk section Tentang PKUKOS
  const aboutData = {
    title: "PKUKOS - Aplikasi Anak Kos di Pekanbaru",
    description: "PKUKOS adalah platform digital yang dirancang khusus untuk memudahkan pencarian, pemesanan, dan pengelolaan kos-kosan di kota Pekanbaru. Dengan visi menjadi solusi utama anak kos dalam menemukan hunian yang nyaman, aman, dan terjangkau, PKUKOS hadir sebagai jembatan antara pemilik kos dan para pencari tempat tinggal.",
    featuresTitle: "Fitur yang dapat dimanfaatkan di PKUKOS",
    features: [
      {
        title: "Pencarian Cerdas",
        description: "Temukan kos sesuai kriteria dengan filter lokasi, harga, dan fasilitas yang lengkap.",
        icon: "pixelarticons:search"
      },
      {
        title: "Booking Online",
        description: "Proses booking kos dapat dilakukan secara online tanpa perlu datang langsung.",
        icon: "pixelarticons:calendar-check"
      },
      {
        title: "Review Transparan",
        description: "Baca review jujur dari penghuni sebelumnya sebelum memutuskan menyewa.",
        icon: "pixelarticons:heart"
      },
      {
        title: "Pembayaran Digital",
        description: "Sistem pembayaran digital yang aman dan terintegrasi.",
        icon: "pixelarticons:credit-card"
      },
      {
        title: "Manajemen Kos",
        description: "Bagi pemilik kos, kelola properti dan transaksi dengan mudah.",
        icon: "pixelarticons:building-community"
      },
      {
        title: "Customer Support",
        description: "Tim support siap membantu 24/7 untuk masalah seputar kos.",
        icon: "pixelarticons:headset"
      }
    ]
  }

  // State untuk toggle fitur
  const showFeatures = ref(false)

  // Method untuk toggle fitur
  const toggleFeatures = () => {
    showFeatures.value = !showFeatures.value
  }

  // Hero section data
  const heroData = {
    mobile: {
      greeting: "Hai,",
      title: "Lagi cari apa?",
      options: [
        {
          id: 1,
          name: "Kamar Kos",
          image: "https://images.unsplash.com/photo-1560448204-e02f11c3d0e2?ixlib=rb-1.2.1&auto=format&fit=crop&w=200&h=200&q=80",
          link: "/kamar-kos" // Added link property
        },
        {
          id: 2,
          name: "Kontrakan",
          image: "https://images.unsplash.com/photo-1522708323590-d24dbb6b0267?ixlib=rb-1.2.1&auto=format&fit=crop&w=200&h=200&q=80",
          link: "/kontrakan" // Added link property
        },
        {
          id: 3,
          name: "Ruko",
          image: "https://images.unsplash.com/photo-1512917774080-9991f1c4c750?ixlib=rb-1.2.1&auto=format&fit=crop&w=200&h=200&q=80",
          link: "/ruko" // Added link property
        }
      ]
    },
    desktop: {
      title: "Mau Cari Kost?",
      subtitle: "Dapatkan infonya dan langsung sewa di PKUKOS."
    }
  };
</script>

<template>
  <div>
    <!-- Section Hero with Swiper Options -->
    <section class="bg-slate-950 text-white py-8 md:py-12 relative overflow-hidden">
      <!-- Background Image with mobile height adjustment -->
      <div class="absolute inset-0 z-0 h-[40vh] md:h-full">
        <img 
          src="/storage/images/kost-ilustrasi.png" 
          alt="Ilustrasi Kost"
          class="w-full h-full object-cover opacity-100"
        />
        <!-- Darker overlay for mobile -->
        <div class="absolute inset-0 bg-gradient-to-r from-slate-950/90 via-slate-950/80 to-slate-950/50 md:from-slate-950 md:via-slate-950/80 md:to-slate-950/20"></div>
      </div>
      
      <div class="container mx-auto px-4 flex flex-col md:flex-row relative z-10">
        <!-- Text Content -->
        <div class="w-full md:w-1/2 mb-6 md:mb-0">
          <!-- Mobile-only content with Swiper -->
          <div class="block md:hidden">
            <h3 class="text-lg font-medium mb-1">{{ heroData.mobile.greeting }}</h3>
            <h1 class="text-2xl font-bold mb-4">{{ heroData.mobile.title }}</h1>
            
            <!-- Swiper for options -->
            <Swiper
              :modules="[Autoplay]"
              :slides-per-view="2"
              :space-between="5"
              :autoplay="{
                delay: 5000,
                disableOnInteraction: true,
              }"
              class="mb-6"
            >
              <SwiperSlide v-for="option in heroData.mobile.options" :key="option.id">
                <Link :href="option.link" class="block">
                  <div class="flex flex-col items-center">
                    <div class="bg-slate-950/10 rounded-lg p-3 w-full h-full flex items-center justify-center transition-transform hover:scale-105">
                      <img :src="option.image" :alt="option.name" class="w-full h-full object-cover rounded-lg">
                    </div>
                    <span class="text-sm mt-2">{{ option.name }}</span>
                  </div>
                </Link>
              </SwiperSlide>
            </Swiper>
          </div>

          <!-- Desktop content -->
          <div class="hidden md:block">
            <h1 class="text-2xl sm:text-3xl md:text-4xl font-bold leading-tight mb-4">
              {{ heroData.desktop.title }}
            </h1>
            <p class="text-base sm:text-lg md:text-xl mb-6">
              {{ heroData.desktop.subtitle }}
            </p>
          </div>

          <!-- Search Form (hidden on mobile) -->
          <div class="hidden md:flex bg-white rounded-lg p-1 flex flex-col sm:flex-row items-center shadow-md w-full max-w-md">
            <input
              type="text"
              placeholder="Masukkan nama lokasi/area/alamat"
              class="w-full px-4 py-2 text-gray-800 focus:outline-none rounded-md mb-2 sm:mb-0"
              v-model="searchQuery"
            />
            <button
              class="w-full sm:w-auto sm:ml-2 bg-slate-950 hover:bg-slate-700 text-white px-4 py-2 rounded-md"
              @click="handleSearch"
            >
              Cari
            </button>
          </div>
        </div>

        <!-- Empty div to maintain layout balance -->
        <div class="w-full md:w-1/2"></div>
      </div>
    </section>

    <!-- Section Swiper Triple Slider -->
    <section class="bg-slate-950 text-white py-4">
      <div class="container mx-auto px-4">
        <div class="w-full relative">
          <Swiper
            :modules="[Navigation, Autoplay, Pagination]"
            :autoplay="{
              delay: 8000,
              disableOnInteraction: false,
            }"
            :pagination="{ clickable: true }"
            :navigation="{
              nextEl: '.custom-next',
              prevEl: '.custom-prev',
            }"
            :slides-per-view="1"
            :space-between="10"
            :breakpoints="{
              400: { slidesPerView: 1.2 },
              500: { slidesPerView: 1.5 },
              640: { slidesPerView: 2 },
              768: { slidesPerView: 2.5 },
              1024: { slidesPerView: 3 }
            }"
            class="rounded-lg shadow-lg w-full"
          >
            <SwiperSlide>
              <a href="#" class="block">
                <img
                  src="https://static.mamikos.com/uploads/cache/data/event/2025-03-07/bCO9Nn21-540x720.jpg"
                  alt="Ilustrasi Kost 1"
                  class="w-full object-cover rounded-lg hover:opacity-90 transition-opacity"
                />
              </a>
            </SwiperSlide>
            <SwiperSlide>
              <a href="#" class="block">
                <img
                  src="https://static.mamikos.com/uploads/cache/data/event/2025-02-28/lERyQJMW-540x720.jpg"
                  alt="Ilustrasi Kost 2"
                  class="w-full object-cover rounded-lg"
                />
              </a>
            </SwiperSlide>
            <SwiperSlide>
              <a href="#" class="block">
                <img
                  src="https://static.mamikos.com/uploads/cache/data/event/2025-02-27/7GbGtCyA-540x720.jpg"
                  alt="Ilustrasi Kost 3"
                  class="w-full object-cover rounded-lg"
                />
              </a>
            </SwiperSlide>
            <SwiperSlide>
              <a href="#" class="block">
                <img
                  src="https://static.mamikos.com/uploads/cache/data/event/2025-05-28/knGK1r1u-540x720.jpg"              
                  alt="Ilustrasi Kost 4"
                  class="w-full object-cover rounded-lg"
                />
              </a>
            </SwiperSlide>
          </Swiper>
          
          <!-- Navigation - Adjusted for mobile -->
          <div class="flex justify-center items-center mt-4 space-x-4 sm:space-x-6">
            <button class="custom-prev bg-slate-800 hover:bg-slate-700 rounded-full p-2 transition-colors">          
              <Icon icon="pixelarticons:chevron-left" class="w-4 h-4 sm:w-5 sm:h-5"/>
            </button>
            
            <a href="#" class="text-xs sm:text-sm font-medium text-white hover:text-slate-400 transition-colors">
              Lihat semua promo
            </a>
            
            <button class="custom-next bg-slate-800 hover:bg-slate-700 rounded-full p-2 transition-colors">
              <Icon icon="pixelarticons:chevron-right" class="w-4 h-4 sm:w-5 sm:h-5"/>
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Card Section - Made more responsive -->
    <section class="bg-slate-950 text-white py-8">
      <div class="container mx-auto px-4">
        <div class="grid grid-cols-1">
          <div 
            v-for="card in promoCards" 
            :key="card.id"
            class="relative rounded-lg overflow-hidden shadow-lg hover:shadow-xl transition-shadow min-h-44 bg-cover bg-no-repeat"
            :style="{ 
              backgroundImage: `linear-gradient(to right, rgba(30, 41, 59, 0.9) 0%, rgba(30, 41, 59, 0.7) 50%, rgba(30, 41, 59, 0.3) 100%), url(${card.image})`,
              backgroundPosition: 'center',
              backgroundSize: 'cover'
            }"
          >
            <div class="absolute inset-0 bg-gradient-to-r from-slate-900/90 via-slate-900/80 to-slate-900/10"></div>
            
            <div class="relative z-10 p-4 sm:p-6 flex flex-col h-full">
              <!-- Header Section -->
              <div class="flex justify-between items-start mb-1">
                <h1 class="text-lg sm:text-xl font-bold">{{ card.title }}</h1>
              </div>
              
              <!-- Description -->
              <p class="text-slate-200 text-sm sm:text-base mb-3 flex-grow">{{ card.description }}</p>

              <!-- Button -->
              <button type="button" 
                      class="text-slate-950 bg-white hover:bg-slate-200 focus:outline-none focus:ring-1 focus:ring-slate-300 font-medium rounded-lg text-xs sm:text-sm px-4 py-2 sm:px-5 sm:py-2.5 text-center me-2 mb-2 w-40 sm:w-50">
                <Link :href="`/promo/${card.id}`">
                  Pelajari Lebih Lanjut                
                </Link>
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Section Swiper Rekomendasi kos - Improved responsiveness -->
    <section class="bg-slate-950 text-white py-8">
      <div class="container mx-auto px-4">
        <!-- Header - Stacked on mobile -->
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-6 gap-3 sm:gap-0">
          <!-- Title & Dropdown -->
          <div class="flex flex-col sm:flex-row sm:items-center gap-2 sm:gap-4 w-full sm:w-auto">
            <h2 class="text-lg sm:text-xl font-bold">Rekomendasi kos di</h2>
            <select
              v-model="selectedLokasi"
              class="bg-slate-800 text-white px-3 py-1 rounded-md focus:outline-none w-full sm:w-auto"
            >
              <option value="">Semua Lokasi</option>
              <option
                v-for="(item, index) in lokasiUnik"
                :key="index"
                :value="item"
              >
                {{ item }}
              </option>
            </select>
          </div>
          
          <!-- Navigasi Swiper - Adjusted for mobile -->
          <div class="flex gap-2 w-full sm:w-auto justify-end">
            <button
              @click="swiperRef?.slidePrev()"
              class="bg-white text-black px-2 py-1 rounded text-sm sm:text-base"
            >
              <Icon icon="pixelarticons:chevron-left" class="w-4 h-4"/>
            </button>
            <a href="#" class="text-xs sm:text-sm font-medium text-white hover:text-slate-400 transition-colors flex items-center">
              Lihat semua
            </a>
            <button
              @click="swiperRef?.slideNext()"
              class="bg-white text-black px-2 py-1 rounded text-sm sm:text-base"
            >
              <Icon icon="pixelarticons:chevron-right" class="w-4 h-4"/>
            </button>
          </div>
        </div>

        <!-- Swiper Kos - Improved breakpoints -->
        <Swiper
          :modules="[Autoplay, Navigation]"
          :slides-per-view="1"
          :space-between="10"
          :breakpoints="{
            400: { slidesPerView: 1.2 },
            500: { slidesPerView: 1.5 },
            640: { slidesPerView: 2 },
            768: { slidesPerView: 2.5 },
            1024: { slidesPerView: 3.5 }
          }"
          @swiper="onSwiperInit"
          autoplay
          class="pb-8"
        >
          <SwiperSlide
            v-for="kos in filteredKos"
            :key="kos.id"
            class="bg-slate-800 rounded-lg overflow-hidden shadow-md"
          >
            <!-- Image with repeated small watermark using CSS -->
            <div class="relative overflow-hidden">
              <img :src="kos.gambar" class="w-full h-48 object-cover" />
              <div class="watermark-pattern"></div>
            </div>

            <!-- Room Availability Badge -->
            <div class="absolute top-2 right-2">
              <span class="text-xs px-2 py-1 rounded-full flex items-center" 
                    :class="{
                      'bg-green-500 text-white': kos.sisa_kamar > 0,
                      'bg-red-500 text-white': kos.sisa_kamar === 0
                    }">
                <Icon icon="mdi:door" class="mr-1" v-if="kos.sisa_kamar > 0" />
                <Icon icon="mdi:door-closed" class="mr-1" v-else />
                {{ kos.sisa_kamar > 0 ? `${kos.sisa_kamar} Kamar tersisa` : 'Penuh' }}
              </span>
            </div>
            
            <div class="p-4">
              <div class="flex justify-between items-start">
                <h3 class="font-semibold text-lg">{{ kos.nama }}</h3>
                <!-- Gender badge -->
                <span 
                  class="text-xs px-2 py-1 rounded-full"
                  :class="{
                    'bg-blue-500': kos.gender === 'putra',
                    'bg-pink-500': kos.gender === 'putri',
                    'bg-purple-500': kos.gender === 'campur'
                  }"
                >
                  {{ kos.gender === 'putra' ? 'Putra' : kos.gender === 'putri' ? 'Putri' : 'Campur' }}
                </span>
              </div>
              
              <p class="text-sm text-gray-300">{{ kos.lokasi }}</p>
              <p class="mt-2 text-yellow-400">{{ kos.harga }}</p>
              
              <!-- Facilities -->
              <div class="mt-3">
                <p class="text-xs text-gray-400 mb-1">Fasilitas:</p>
                <div class="flex flex-wrap gap-1">
                  <span 
                    v-for="(facility, index) in kos.fasilitas" 
                    :key="index"
                    class="text-xs bg-slate-700 px-2 py-1 rounded"
                  >
                    {{ facility }}
                  </span>
                </div>
              </div>
            </div>
          </SwiperSlide>
        </Swiper>
      </div>
    </section>

    <!-- Section Tentang PKUKOS - Made more responsive -->
    <section class="bg-slate-950 text-white py-8">
      <div class="container mx-auto px-4 mb-8">
        <!-- Header -->
        <div class="flex justify-center items-center mb-6">
          <div class="flex items-center">
            <h1 class="text-xl sm:text-2xl font-bold text-white text-center">{{ aboutData.title }}</h1>
          </div>          
        </div>
        <div class="flex justify-start items-center">
          <div class="flex items-center">
            <span class="text-sm sm:text-base md:text-xl text-justify">{{ aboutData.description }}</span>
          </div>
        </div>
        
        <!-- Fitur Unggulan - Improved mobile layout -->
        <div class="mt-8">
          <button 
            @click="toggleFeatures" 
            class="w-full text-center mb-4"
          >
            <h1 class="text-lg sm:text-xl font-semibold flex justify-center items-center hover:text-slate-400">
              {{ aboutData.featuresTitle }}
              <Icon 
                :icon="showFeatures ? 'pixelarticons:chevron-up' : 'pixelarticons:chevron-down'" 
                class="ml-2 text-white hover:text-slate-400"
              />
            </h1>
          </button>
          
          <!-- Fitur yang bisa di-toggle - Adjusted grid for mobile -->
          <div v-if="showFeatures" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3 sm:gap-4">
            <div v-for="(feature, index) in aboutData.features" :key="index" class="bg-slate-800 p-3 sm:p-4 rounded-lg">
              <div class="flex items-center mb-2">
                <Icon :icon="feature.icon" class="text-blue-400 text-xl sm:text-2xl mr-2" />
                <h3 class="font-medium text-sm sm:text-base">{{ feature.title }}</h3>
              </div>
              <p class="text-slate-300 text-xs sm:text-sm">{{ feature.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
  .watermark-pattern {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><text x="10" y="50" font-family="Arial" font-size="12" fill="white" transform="rotate(-30 50,50)">PKUKOS</text></svg>');
    background-repeat: repeat;
    opacity: 0.2;
    pointer-events: none;
  }

  /* Responsive adjustments for very small screens */
  @media (max-width: 400px) {
    .container {
      padding-left: 1rem;
      padding-right: 1rem;
    }
  }
</style>
