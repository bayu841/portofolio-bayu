<script setup>
import { ref, onMounted } from "vue";
import ElectricBorder from '../components/common/ElectricBorder.vue';

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
      id="workflow"
      :class="[
        'text-white py-28 md:py-32 px-6 font-poppins bg-gray-900/40 transition-all duration-700',
        isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-16'
      ]"
    >
    <div class="max-w-6xl mx-auto">
      
      <!-- TITLE -->
      <div class="text-center mb-10">
        <h1 class="text-4xl font-bold mb-2 text-gradient">
          Bagaimana Saya Bekerja ?
        </h1>
        <p class="text-gray-400 mx-auto text-base lg:text-sm">
          Berikut cara saya bekerja untuk menciptakan website yang menarik dan fungsional.
        </p>
      </div>

      <!-- Workflow -->
      <div class="relative">

        <!-- LINE -->
        <div class="hidden md:block absolute top-1/2 left-0 w-full h-[2px] bg-white/10"></div>

        <div class="grid md:grid-cols-3 gap-10 mb-4 relative">

          <!-- STEP 1 -->
          <div class="text-center group">
            
            <!-- ICON -->
            <div class="w-14 h-14 mx-auto rounded-full bg-blue-800 flex items-center justify-center shadow-lg
                        group-hover:scale-110 transition">
              <i class="pi pi-lightbulb text-white text-xl"></i>
            </div>

            <!-- ELECTRIC CARD -->
            <ElectricBorder
              color="#3b82f6"
              :speed="1"
              :chaos="0.5"
              :thickness="2"
              class="mt-6 block"
              :style="{ borderRadius: '16px' }"
            >
              <div class="bg-gray-800/70 backdrop-blur p-6 rounded-xl cursor-target">
                <h3 class="font-semibold mb-2">Ide & Konsep</h3>
                <p class="text-gray-400 text-sm">
                  Memahami kebutuhan klien dan merancang konsep desain yang sesuai.
                </p>
              </div>
            </ElectricBorder>

          </div>

          <!-- STEP 2 -->
          <div class="text-center group">
            
            <div class="w-14 h-14 mx-auto rounded-full bg-purple-800 flex items-center justify-center shadow-lg
                        group-hover:scale-110 transition">
              <i class="pi pi-pencil text-white text-xl"></i>
            </div>

            <ElectricBorder
              color="#a855f7"
              :speed="1"
              :chaos="0.5"
              :thickness="2"
              class="mt-6 block"
              :style="{ borderRadius: '16px' }"
            >
              <div class="bg-gray-800/70 backdrop-blur p-6 rounded-xl cursor-target">
                <h3 class="font-semibold mb-2">Desain & Prototipe</h3>
                <p class="text-gray-400 text-sm">
                  Membuat desain visual dan prototipe interaktif untuk validasi.
                </p>
              </div>
            </ElectricBorder>

          </div>

          <!-- STEP 3 -->
          <div class="text-center group">
            
            <div class="w-14 h-14 mx-auto rounded-full bg-green-800 flex items-center justify-center shadow-lg
                        group-hover:scale-110 transition">
              <i class="pi pi-cog text-white text-xl"></i>
            </div>

            <ElectricBorder
              color="#22c55e"
              :speed="1"
              :chaos="0.5"
              :thickness="2"
              class="mt-6 block"
              :style="{ borderRadius: '16px' }"
            >
              <div class="bg-gray-800/70 backdrop-blur p-6 rounded-xl cursor-target">
                <h3 class="font-semibold mb-2">Pengembangan & Peluncuran</h3>
                <p class="text-gray-400 text-sm">
                  Mengembangkan website dengan teknologi modern dan meluncurkannya.
                </p>
              </div>
            </ElectricBorder>

          </div>

        </div>
      </div>
    </div>
  </section>
</template>