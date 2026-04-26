<script setup>
import { ref, onMounted } from "vue";

const experiences = [
  {
    role: "Fresh Graduate",
    company: "-",
    time: "2026 - Sekarang",
    desc: "Membangun website modern menggunakan Vue, Tailwind, dan animasi interaktif."
  },
  {
    role: "PKL Frontend Developer",
    company: "PT Mascitra.com",
    time: "2025 - 2026",
    desc: "Mengembangkan fitur website company profile dan sistem admin berbasis Laravel."
  },
  {
    role: "Pelajar",
    company: "majoring in software engineering",
    time: "2023 - 2024",
    desc: "Mendalami HTML, CSS, JavaScript, dan mulai masuk ke framework modern."
  }
];

const sectionRef = ref(null);
const isVisible = ref(false);

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isVisible.value = true;
      }
    },
    { threshold: 0.2 }
  );

  if (sectionRef.value) observer.observe(sectionRef.value);
});
</script>

<template>
    <section
    ref="sectionRef"
    id="experience"
    :class="[
        'text-white py-20 md:py-32 px-6 font-poppins transition-all duration-700',
        isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-16'
    ]"
    >
    <div class="max-w-5xl mx-auto">

      <!-- TITLE -->
      <div class="text-center mb-16">
        <h1 class="text-3xl md:text-4xl font-bold text-gradient mb-2">
          Pengalaman Saya
        </h1>
        <p class="text-gray-400 text-base lg:text-sm">
          Perjalanan saya dalam dunia pengembangan web.
        </p>
      </div>

      <!-- TIMELINE -->
      <div class="relative">

        <!-- LINE -->
        <div class="absolute left-4 md:left-1/2 md:-translate-x-1/2 top-0 w-[2px] h-full bg-white/10"></div>

        <div class="space-y-12 ">

          <div
            v-for="(exp, i) in experiences"
            :key="i"
            class="relative flex flex-col md:flex-row items-start md:items-center"
          >

            <!-- DOT -->
            <div class="absolute left-4 md:left-1/2 md:-translate-x-1/2 w-4 h-4 bg-blue-500 rounded-full border-4 border-gray-900 "></div>

            <!-- CARD -->
            <div
              :class="[
                'mt-6 md:mt-0 md:w-1/2 cursor-target',
                i % 2 === 0 ? 'md:pr-10 md:text-right' : 'md:pl-10 md:ml-auto '
              ]"
            >
              <div
                class="bg-gray-800/60 backdrop-blur p-6 rounded-xl border border-white/10 hover:border-blue-400 transition"
              >
                <h3 class="text-lg font-semibold">{{ exp.role }}</h3>
                <p class="text-sm text-blue-400 mb-1">{{ exp.company }}</p>
                <span class="text-xs text-gray-500">{{ exp.time }}</span>

                <p class="text-gray-400 text-sm mt-3">
                  {{ exp.desc }}
                </p>
              </div>
            </div>

          </div>

        </div>
      </div>
    </div>
  </section>
</template>