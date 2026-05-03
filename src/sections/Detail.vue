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
      "Project ini dibuat untuk membantu pengguna belajar coding secara interaktif dengan tampilan modern dan responsif.",
    tools: ["Vue", "Tailwind", "JavaScript"],
    image: `${import.meta.env.BASE_URL}images/project/project1.webp`,
  },
  {
    id: 2,
    title: "Perpustakaan Digital",
    detail:
      "Aplikasi ini memungkinkan pengguna untuk mengelola data buku, peminjaman, dan laporan secara efisien.",
    tools: ["Laravel", "Bootstrap", "MySQL"],
    image: `${import.meta.env.BASE_URL}images/project/project2.webp`,
  },
  {
    id: 3,
    title: "Manajemen Toko",
    detail:
      "Digunakan untuk mencatat transaksi penjualan, mengelola stok barang, serta menghasilkan laporan otomatis.",
    tools: ["Laravel", "Tailwind", "MySQL"],
    image: `${import.meta.env.BASE_URL}images/project/project3.webp`,
  },
];

const projectId = Number(route.params.id);

const project = computed(() => {
  return projects.find((p) => p.id == route.params.id);
});
</script>

<template>
  <section class="text-white px-6 sm:px-6 py-[170px] sm:py-[120px]">
    <div v-if="project" :key="route.params.id" class="max-w-4xl mx-auto">
      <!-- IMAGE -->
      <img
        :src="project.image"
        class="rounded-xl mb-5 sm:mb-6 w-full h-52 sm:h-64 md:h-72 object-cover cursor-target"
      />

      <!-- TITLE -->
      <h1 class="text-2xl sm:text-3xl font-bold mb-3 sm:mb-4">
        {{ project.title }}
      </h1>

      <p class="text-gray-300 text-sm sm:text-sm mb-6 leading-relaxed">
        {{ project.detail }}
      </p>

      <div class="mb-3">
        <div class="flex flex-wrap gap-2">
          <span
            v-for="tool in project.tools"
            :key="tool"
            class="px-3 py-1 text-xs sm:text-sm bg-gray-800 hover:bg-gray-700 text-white rounded-full border border-white/10 transition"
          >
            {{ tool }}
          </span>
        </div>
      </div>
      <button
        @click="router.back()"
        class="mt-6 inline-flex items-center gap-2 px-4 py-2 rounded-lg bg-gray-800 hover:bg-gray-700 text-sm text-white transition cursor-target"
      >
        <span>←</span> Kembali
      </button>
    </div>

    <!-- NOT FOUND -->
    <div v-else class="text-center text-gray-400 text-sm sm:text-base">
      Project tidak ditemukan
    </div>
  </section>
</template>
