<script setup>
import { computed } from "vue";
import { useRouter, useRoute } from "vue-router";

const router = useRouter();
const route = useRoute();

const projects = [
  {
    id: 1,
    title: "Zona Coding",
    detail:
      "Project ini dibuat untuk membantu pengguna belajar coding secara interaktif melalui pengalaman belajar yang lebih modern, nyaman, dan mudah dipahami. Platform ini menghadirkan antarmuka yang responsif sehingga dapat digunakan dengan baik di berbagai perangkat, mulai dari desktop hingga smartphone. Dengan desain yang bersih dan intuitif, pengguna dapat fokus pada proses belajar tanpa terganggu oleh tampilan yang rumit.",
    tools: ["Vue", "Tailwind"],
    image: `${import.meta.env.BASE_URL}images/project/project1.webp`,
  },
  {
    id: 2,
    title: "Perpustakaan Digital",
    detail:
      "Aplikasi ini memungkinkan pengguna untuk membaca buku secara digital dengan lebih mudah, praktis, dan fleksibel melalui berbagai perangkat. Dengan tampilan yang modern dan responsif, pengguna dapat menikmati pengalaman membaca yang nyaman baik di desktop maupun smartphone tanpa kehilangan kualitas antarmuka.",
    tools: ["Laravel", "Bootstrap", "MySQL"],
    image: `${import.meta.env.BASE_URL}images/project/project2.webp`,
  },
  {
    id: 3,
    title: "Manajemen Toko",
    detail:
      "Aplikasi ini digunakan untuk membantu proses pengelolaan penjualan secara lebih efektif dan terstruktur. Sistem memungkinkan pengguna untuk mencatat setiap transaksi penjualan dengan mudah, sehingga data penjualan dapat tersimpan secara rapi dan terorganisir dalam database.",
    tools: ["Laravel", "Bootstrap", "MySQL"],
    image: `${import.meta.env.BASE_URL}images/project/project3.webp`,
  },
];

const project = computed(() => {
  return projects.find((p) => p.id == route.params.id);
});
</script>

<template>
  <section
    class="min-h-screen text-white px-5 sm:px-8 py-[130px] relative overflow-hidden"
  >
    <!-- BACKGROUND BLUR -->
    <div
      class="absolute top-20 left-1/2 -translate-x-1/2 w-[500px] h-[500px] bg-blue-500/10 blur-[140px] rounded-full"
    ></div>

    <div
      v-if="project"
      :key="route.params.id"
      class="max-w-5xl mx-auto relative z-10"
    >
      <!-- CARD -->
      <div
        class="bg-white/5 border border-white/10 backdrop-blur-xl rounded-3xl overflow-hidden shadow-2xl"
      >
        <!-- IMAGE -->
        <div class="relative group overflow-hidden">
          <img
            :src="project.image"
            class="w-full h-[230px] sm:h-[320px] md:h-[420px] object-cover transition duration-700 group-hover:scale-105"
          />

          <!-- OVERLAY -->
          <div
            class="absolute inset-0 bg-gradient-to-t from-black/70 via-black/20 to-transparent"
          ></div>

          <!-- TITLE ON IMAGE -->
          <div class="absolute bottom-0 left-0 p-6 sm:p-8">
            <p
              class="text-xs uppercase tracking-[4px] text-gray-300 mb-2 font-medium"
            >
              Featured Project
            </p>

            <h1
              class="text-3xl sm:text-4xl md:text-5xl font-bold leading-tight"
            >
              {{ project.title }}
            </h1>
          </div>
        </div>

        <!-- CONTENT -->
        <div class="p-6 sm:p-8 md:p-10">
          <!-- DESCRIPTION -->
          <div class="mb-8 cursor-target">
            <h2 class="text-lg sm:text-2xl font-semibold mb-4 text-white">
              Tentang Project
            </h2>

            <p
              class="text-gray-300 leading-relaxed text-sm sm:text-sm tracking-wide"
            >
              {{ project.detail }}
            </p>
          </div>

          <!-- TOOLS -->
          <div class="mb-8">
            <div class="flex flex-wrap gap-3">
              <span
                v-for="tool in project.tools"
                :key="tool"
                class="px-4 py-2 rounded-full bg-gray-800 border-white/10 text-sm hover:scale-105 transition duration-300 cursor-target"
              >
                {{ tool }}
              </span>
            </div>
          </div>

          <!-- BUTTON -->
          <button
            @click="router.back()"
            class="group inline-flex items-center gap-3 px-4 py-2 rounded-xl button-gradient text-white font-medium hover:scale-105 transition duration-300 cursor-target"
          >
            <span
              class="group-hover:-translate-x-1 transition duration-300"
            >
              ←
            </span>

            Kembali
          </button>
        </div>
      </div>
    </div>

    <!-- NOT FOUND -->
    <div
      v-else
      class="text-center text-gray-400 text-sm sm:text-base relative z-10"
    >
      Project tidak ditemukan
    </div>
  </section>
</template>