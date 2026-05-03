<script setup>
import { ref, onMounted } from "vue";
import { useRouter, useRoute } from "vue-router";

const router = useRouter();
const route = useRoute();

const isOpen = ref(false);
const showNavbar = ref(false); 

onMounted(() => {
  setTimeout(() => {
    showNavbar.value = true;
  }, 400); 
});


const toggleMenu = () => {
  isOpen.value = !isOpen.value;
};

const scrollTo = async (id) => {
  if (route.path !== "/") {
    await router.push("/");

    setTimeout(() => {
      const el = document.getElementById(id);
      if (el) {
        el.scrollIntoView({ behavior: "smooth" });
      }
    }, 300);
  } else {
    const el = document.getElementById(id);
    if (el) {
      el.scrollIntoView({ behavior: "smooth" });
    }
  }

  isOpen.value = false;
};
</script>

<template>
  <Transition name="nav">
  <nav
  v-if="showNavbar"
  class="fixed top-2 left-1/2 -translate-x-1/2 z-50
         w-[92%] max-w-6xl
         text-white font-poppins
         bg-gray-900/60 backdrop-blur-md
         border border-white/10
         rounded-[24px] md:rounded-[200px] shadow-lg text-sm"
>
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 ">
      <div class="flex justify-between items-center h-14 cursor-target">
        <!-- Logo -->
        <div class="flex items-center">
          <span class="text-[16px] font-bold w-0">@Bayu_A</span>
        </div>

        <!-- Desktop Menu -->
        <div class="hidden md:flex space-x-6">
          <button
            @click="scrollTo('hero')"
            class="relative hover:text-blue-400 transition after:content-[''] after:absolute after:left-0 after:-bottom-1 after:h-[2px] after:w-0 after:bg-blue-400 after:transition-all after:duration-300 hover:after:w-full"
          >
            Beranda
          </button>

          <button
            @click="scrollTo('about')"
            class="relative hover:text-blue-400 transition after:content-[''] after:absolute after:left-0 after:-bottom-1 after:h-[2px] after:w-0 after:bg-blue-400 after:transition-all after:duration-300 hover:after:w-full"
          >
            Tentang
          </button>

          <button
            @click="scrollTo('projects')"
            class="relative hover:text-blue-400 transition after:content-[''] after:absolute after:left-0 after:-bottom-1 after:h-[2px] after:w-0 after:bg-blue-400 after:transition-all after:duration-300 hover:after:w-full"
          >
            Projek
          </button>

          <button
            @click="scrollTo('workflow')"
            class="relative hover:text-blue-400 transition after:content-[''] after:absolute after:left-0 after:-bottom-1 after:h-[2px] after:w-0 after:bg-blue-400 after:transition-all after:duration-300 hover:after:w-full"
          >
            Alur Kerja
          </button>

          <button
            @click="scrollTo('experience')"
            class="relative hover:text-blue-400 transition after:content-[''] after:absolute after:left-0 after:-bottom-1 after:h-[2px] after:w-0 after:bg-blue-400 after:transition-all after:duration-300 hover:after:w-full"
          >
            Pengalaman
          </button>

          <button
            @click="scrollTo('contact')"
            class="relative hover:text-blue-400 transition after:content-[''] after:absolute after:left-0 after:-bottom-1 after:h-[2px] after:w-0 after:bg-blue-400 after:transition-all after:duration-300 hover:after:w-full"
          >
            Kontak
          </button>
        </div>

        <!-- Right Section -->
        <div class="flex items-center space-x-4">
          <!-- Profile -->
          <img
            src="/images/avatar.webp"
            class="w-8 h-8 rounded-full border border-gray-600"
          />

          <!-- Mobile Button -->
          <button @click="toggleMenu" class="md:hidden focus:outline-none">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M4 6h16M4 12h16M4 18h16"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Menu -->
    <Transition name="mobile">
      <div
        v-if="isOpen"
        class="md:hidden px-4 pb-4 space-y-2 m-4 rounded-2xl bg-gray-800"
      >
        <button @click="scrollTo('hero')" class="block py-2 w-full text-left">
          Beranda
        </button>
        <button @click="scrollTo('about')" class="block py-2 w-full text-left">
          Tentang
        </button>
        <button
          @click="scrollTo('projects')"
          class="block py-2 w-full text-left">
          Projek
        </button>
        <button
          @click="scrollTo('workflow')"
          class="block py-2 w-full text-left">
          Alur Kerja
        </button>
       
        <button
          @click="scrollTo('contact')"
          class="block py-2 w-full text-left"
        >
          Kontak
        </button>
      </div>
    </Transition>
  </nav>
  </Transition>
</template>
