<script setup>
import { ref, computed, onMounted } from "vue";
import GlareHover from "../components/common/GlareHover.vue";

const activeTab = ref("projects");

const projects = [
  { id:1, title: "Zona Coding - Academy (UI)", desc: "Vue.js", image: "images/project/project1.webp" },
  { id:2, title: "Perpustakaan Digital", desc: "Laravel", image: "images/project/project2.webp" },
  { id:3, title: "Manajemen Toko", desc: "Laravel", image: "images/project/project3.webp" },
  { id:4, title: "E-Commerce Taman (Figma)", desc: "Figma", image: "images/project/project4.webp" },
  { id:5, title: "SI RATU (Persuratan Terpadu)", desc: "Figma + Vue.js", image: "images/project/project5.webp" },
];

const certificates = [
  { image: "images/cert1.webp" },
  { image: "images/cert2.webp" },
  { image: "images/cert3.webp" },
  { image: "images/cert4.webp" },
  { image: "images/cert5.webp" },
];

const skills = [
  { name: "HTML", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" },
  { name: "CSS", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg" },
  { name: "Vue", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg" },
  { name: "Tailwind", icon: "https://www.vectorlogo.zone/logos/tailwindcss/tailwindcss-icon.svg" },
  { name: "Laravel", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-original.svg" },
  { name: "Figma", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg" },
  { name: "Bootstrap", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bootstrap/bootstrap-original.svg" },
];

// Slider state
const currentSlide = ref(0);
const slidesPerView = ref(1);
const isTransitioning = ref(false);

// Hitung jumlah slide berdasarkan lebar layar
const updateSlidesPerView = () => {
  const width = window.innerWidth;
  if (width >= 1024) {
    slidesPerView.value = 3;
  } else if (width >= 768) {
    slidesPerView.value = 2;
  } else {
    slidesPerView.value = 1;
  }
  // Reset current slide agar tidak melebihi batas
  const maxSlide = Math.max(0, projects.length - slidesPerView.value);
  if (currentSlide.value > maxSlide) {
    currentSlide.value = maxSlide;
  }
};

// Total slide groups
const totalSlides = computed(() => {
  return Math.max(0, projects.length - slidesPerView.value);
});

// Next slide
const nextSlide = () => {
  if (isTransitioning.value) return;
  if (currentSlide.value < totalSlides.value) {
    isTransitioning.value = true;
    currentSlide.value++;
    setTimeout(() => {
      isTransitioning.value = false;
    }, 500);
  }
};

// Previous slide
const prevSlide = () => {
  if (isTransitioning.value) return;
  if (currentSlide.value > 0) {
    isTransitioning.value = true;
    currentSlide.value--;
    setTimeout(() => {
      isTransitioning.value = false;
    }, 500);
  }
};

// Go to specific slide
const goToSlide = (index) => {
  if (isTransitioning.value) return;
  if (index >= 0 && index <= totalSlides.value) {
    isTransitioning.value = true;
    currentSlide.value = index;
    setTimeout(() => {
      isTransitioning.value = false;
    }, 500);
  }
};

// Visible projects for current slide
const visibleProjects = computed(() => {
  const start = currentSlide.value;
  const end = start + slidesPerView.value;
  return projects.slice(start, end);
});

const tabClass = (tab) => {
  return [
    "px-6 py-2 rounded-lg text-sm transition",
    activeTab.value === tab
      ? "categories-gradient text-white"
      : "text-gray-400 hover:text-white",
  ];
};

const currentContent = computed(() => {
  if (activeTab.value === "projects") return projects;
  if (activeTab.value === "certificates") return certificates;
  return skills;
});

const sectionRef = ref(null);
const isVisible = ref(false);

onMounted(() => {
  updateSlidesPerView();
  window.addEventListener("resize", updateSlidesPerView);
  
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isVisible.value = true;
      }
    },
    { threshold: 0.1 }
  );

  if (sectionRef.value) {
    observer.observe(sectionRef.value);
  }
});
</script>

<template>
  <section
    ref="sectionRef"
    id="projects"
    :class="[
      'text-white py-32 sm:py-20 md:py-20 px-6 transition-all duration-700 mb-20',
      isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
    ]"
  >
    <!-- TITLE -->
    <div class="text-center mb-10">
      <h1 class="text-4xl font-bold mb-2 text-gradient">Portfolio & Karya</h1>
      <p class="text-gray-400 max-w-xl mx-auto text-base lg:text-sm">
        Jelajahi proyek, sertifikat, dan keterampilan teknis saya.
      </p>
    </div>

    <!-- TAB MENU -->
    <div class="flex justify-center mb-10 px-4 sm:px-0">
      <div
        class="bg-gray-900/60 p-2 rounded-xl flex gap-1 sm:gap-1 backdrop-blur cursor-target"
      >
        <button
          @click="activeTab = 'projects'"
          :class="tabClass('projects')"
          class="px-3 py-1.5 sm:px-4 sm:py-2"
        >
          Projek
        </button>

        <button
          @click="activeTab = 'certificates'"
          :class="tabClass('certificates')"
          class="px-3 py-1.5 sm:px-4 sm:py-2"
        >
          Sertifikat
        </button>

        <button
          @click="activeTab = 'skills'"
          :class="tabClass('skills')"
          class="px-3 py-1.5 sm:px-4 sm:py-2"
        >
          Skill
        </button>
      </div>
    </div>

    <!-- CONTENT -->
    <div class="max-w-6xl mx-auto">
      <Transition name="pop" mode="out-in">
        <div :key="activeTab">
          <!-- PROJECT SLIDER -->
          <div v-if="activeTab === 'projects'" class="relative">
            <!-- Slider Container -->
            <div class="overflow-hidden px-2">
              <div 
                class="flex transition-transform duration-500 ease-out"
                :style="{ transform: `translateX(-${currentSlide * (100 / slidesPerView)}%)` }"
              >
                <div
                  v-for="(project, i) in projects"
                  :key="i"
                  class="flex-shrink-0 px-2"
                  :style="{ width: `${100 / slidesPerView}%` }"
                >
                  <GlareHover
                    class="w-full cursor-target h-full"
                    width="100%"
                    height="100%"
                    background="rgba(17, 24, 39, 0.5)"
                    border-color="#111827"
                    border-radius="12px"
                    glare-color="#ffffff"
                    :glare-opacity="0.25"
                    :glare-size="250"
                    :transition-duration="600"
                    :play-once="false"
                  >
                    <div class="rounded-xl p-2 shadow-lg h-full flex flex-col">
                      <img
                        :src="project.image"
                        class="rounded-lg mb-4 w-full h-40 object-cover"
                        :alt="project.title"
                      />
                      <h3 class="font-normal text-normal sm:text-sm pl-2 mb-1">
                        {{ project.title }}
                      </h3>
                      <p class="text-gray-400 text-xs sm:text-sm pl-2">
                        {{ project.desc }}
                      </p>
                      <div class="flex justify-end pl-2 mt-auto pt-2">
                        <RouterLink 
                          :to="`/detail/${project.id}`" 
                          class="text-blue-500 hover:text-blue-300 text-sm font-medium"
                        >
                          Detail ->
                        </RouterLink>
                      </div>
                    </div>
                  </GlareHover>
                </div>
              </div>
            </div>

            <!-- Navigation Buttons -->
            <button
              @click="prevSlide"
              :disabled="currentSlide === 0"
              class="absolute left-0 top-1/2 -translate-y-1/2 -translate-x-2 lg:-translate-x-4 bg-gray-800/80 hover:bg-gray-700 rounded-full p-2 backdrop-blur transition-all duration-200 disabled:opacity-30 disabled:cursor-not-allowed z-10"
              :class="{ 'opacity-50 cursor-not-allowed': currentSlide === 0 }"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 sm:h-6 sm:w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
              </svg>
            </button>
            <button
              @click="nextSlide"
              :disabled="currentSlide >= totalSlides"
              class="absolute right-0 top-1/2 -translate-y-1/2 translate-x-2 lg:translate-x-4 bg-gray-800/80 hover:bg-gray-700 rounded-full p-2 backdrop-blur transition-all duration-200 disabled:opacity-30 disabled:cursor-not-allowed z-10"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 sm:h-6 sm:w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </button>

            <!-- Dots Indicator -->
            <div v-if="totalSlides > 0" class="flex justify-center gap-2 mt-6">
              <button
                v-for="n in totalSlides + 1"
                :key="n - 1"
                @click="goToSlide(n - 1)"
                class="transition-all duration-200 rounded-full"
                :class="[
                  currentSlide === n - 1 
                    ? 'w-8 h-2 bg-blue-500' 
                    : 'w-2 h-2 bg-gray-500 hover:bg-gray-400'
                ]"
              ></button>
            </div>
          </div>

          <!-- CERTIFICATE -->
          <div
            v-else-if="activeTab === 'certificates'"
            class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-3 gap-6"
          >
            <div
              v-for="(cert, i) in certificates"
              :key="i"
              class="bg-gray-900/50 rounded-xl p-1 shadow-lg cursor-target"
            >
              <img :src="cert.image" class="rounded-lg w-full h-auto" :alt="`Certificate ${i + 1}`" />
            </div>
          </div>

          <!-- SKILLS -->
          <div v-else class="grid grid-cols-2 md:grid-cols-4 gap-6">
            <GlareHover
              v-for="(skill, i) in skills"
              :key="i"
              width="100%"
              height="160px"
              background="#111827"
              border-color="#111827"
              border-radius="16px"
              glare-color="#ffffff"
              :glare-opacity="0.2"
              :glare-size="200"
              class="cursor-target"
            >
              <div
                class="flex flex-col items-center justify-center h-full text-white"
              >
                <img :src="skill.icon" class="w-12 h-12 mb-3" :alt="skill.name" />
                <p class="text-sm text-gray-300">{{ skill.name }}</p>
              </div>
            </GlareHover>
          </div>
        </div>
      </Transition>
    </div>
  </section>
</template>

<style scoped>
.transition-transform {
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}

.overflow-hidden {
  -webkit-overflow-scrolling: touch;
}
</style>