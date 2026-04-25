<script setup>
import { ref, computed, onMounted } from "vue";
import GlareHover from "../components/common/GlareHover.vue";
const activeTab = ref("projects");

// DATA PROJECT
const projects = [
  { title: "Zona Coding - Academy (UI)", desc: "Vue.js", image: "/images/project/project1.webp" },
  { title: "Perpustakaan Digital", desc: "Laravel", image: "/images/project/project2.webp" },
  { title: "Manajemen Toko", desc: "Laravel", image: "/images/project/project3.webp" },
  { title: "E-Commerce Taman (Figma)", desc: "Figma", image: "/images/project/project4.webp" },
  { title: "SI RATU (Persuratan Terpadu)", desc: "Figma + Vue.js", image: "/images/project/project5.webp" },
];

// DATA CERTIFICATE
const certificates = [
  { image: "/images/cert1.webp" },
  { image: "/images/cert2.webp" },
  { image: "/images/cert3.webp" },
  { image: "/images/cert4.webp" },
];

// DATA SKILLS
const skills = [
  { name: "HTML", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" },
  { name: "CSS", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg" },
  { name: "Vue", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg" },
  { name: "Tailwind", icon: "https://www.vectorlogo.zone/logos/tailwindcss/tailwindcss-icon.svg" },
  { name: "Laravel", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-original.svg" },
  { name: "Figma", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/figma/figma-original.svg" },
  { name: "Bootstrap", icon: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bootstrap/bootstrap-original.svg" },
];

// TAB CLASS (FIX UTAMA ADA DI SINI)
const tabClass = (tab) => {
  return [
    "px-6 py-2 rounded-lg text-sm transition",
    activeTab.value === tab
      ? "categories-gradient text-white"
      : "text-gray-400 hover:text-white",
  ];
};

// CONTENT DINAMIS
const currentContent = computed(() => {
  if (activeTab.value === "projects") return projects;
  if (activeTab.value === "certificates") return certificates;
  return skills;
});

// ANIMATION SCROLL
const sectionRef = ref(null);
const isVisible = ref(false);

onMounted(() => {
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
      'text-white py-20 px-6 transition-all duration-700',
      isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'
    ]"
  >

    <!-- TITLE -->
    <div class="text-center mb-12">
      <h1 class="text-4xl font-bold mb-2 text-gradient">
        Portfolio Showcase
      </h1>
      <p class="text-gray-400 max-w-xl mx-auto">
        Explore my projects, certificates, and technical skills.
      </p>
    </div>

    <!-- TAB MENU -->
    <div class="flex justify-center mb-10">
      <div class="bg-gray-900/60 p-2 rounded-xl flex gap-2 backdrop-blur">

        <button @click="activeTab = 'projects'" :class="tabClass('projects')">
          Projects
        </button>

        <button @click="activeTab = 'certificates'" :class="tabClass('certificates')">
          Certificates
        </button>

        <button @click="activeTab = 'skills'" :class="tabClass('skills')">
          Skills
        </button>

      </div>
    </div>

    <!-- CONTENT -->
    <div class="max-w-6xl mx-auto">

      <Transition name="pop" mode="out-in">
        <div :key="activeTab">

          <!-- PROJECT -->
       <div v-if="activeTab === 'projects'" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
          <GlareHover
            v-for="(project, i) in projects"
            :key="i"
            class="w-full"
            width="100%"
            height="255px"
            background="rgba(17, 24, 39, 0.5)"
            border-color="#111827"
            border-radius="12px"
            glare-color="#ffffff"
            :glare-opacity="0.25"
            :glare-size="250"
            :transition-duration="600"
            :play-once="false"
          >
            <!-- ISI ORIGINAL STYLE KAMU DIPERTAHANKAN -->
            <div class="rounded-xl p-3 shadow-lg h-full flex flex-col">

              <img
                :src="project.image"
                class="rounded-lg mb-4 w-full h-40 object-cover"
              />

              <h3 class="font-normal text-base sm:text-lg pl-2 mb-1">
                {{ project.title }}
              </h3>

              <p class="text-gray-400 text-sm pl-2">
                {{ project.desc }}
              </p>

            </div>
          </GlareHover>
        </div>
          <!-- CERTIFICATE -->
          <div v-else-if="activeTab === 'certificates'" class="grid md:grid-cols-3 gap-6">
            <div
              v-for="(cert, i) in certificates"
              :key="i"
              class="bg-gray-900/50 rounded-xl p-2 shadow-lg"
            >
              <img :src="cert.image" class="rounded-lg" />
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
            >
              <div class="flex flex-col items-center justify-center h-full text-white">
                <img :src="skill.icon" class="w-12 h-12 mb-3" />
                <p class="text-sm text-gray-300">{{ skill.name }}</p>
              </div>
        </GlareHover>
          </div>

        </div>
      </Transition>

    </div>
  </section>
</template>