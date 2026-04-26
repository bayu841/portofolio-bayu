<script setup lang="ts">
import { ref, onMounted } from "vue";
import ProfileCard from "../components/common/ProfileCard.vue";
import profile from "../assets/images/profile.webp";
import pattern from "../assets/images/iconpattern.webp";
import grain from "../assets/images/grain.webp";


const isMobile = ref(false);

const sectionRef = ref<HTMLElement | null>(null);
const isVisible = ref(false);

onMounted(() => {
  isMobile.value = window.innerWidth < 768;

  if (isMobile.value) {
    isVisible.value = true;
    return;
  }

  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isVisible.value = true;
        observer.disconnect(); 
      }
    },
    { threshold: 0.1 }
  );

  if (sectionRef.value) {
    observer.observe(sectionRef.value);
  }
});
const handleContactClick = () => {
  console.log("Contact clicked");
};
</script>

<template>
  <section
    ref="sectionRef"
    id="about"
    class="text-white py-22 md:py-28 px-6 font-poppins transition-all duration-700 will-change-transform"
    :class="
      isVisible
        ? 'opacity-100 translate-y-0'
        : 'opacity-0 translate-y-5 md:translate-y-10'
    "
  >
    <!-- Content -->
    <div
      class="max-w-7xl mx-auto grid md:grid-cols-2 gap-10 md:gap-12 items-center"
    >
      <!-- LEFT: CARD -->
      <div class="flex justify-center">
        <ProfileCard
          name="Bayu"
          title="Frontend Enthusiast"
          handle="bayu_a"
          status="Online"
          contact-text="Hi Everyone!🙌"
          :avatar-url="profile"
          :icon-url="pattern"
          :grain-url="grain"
          :show-user-info="true"
          :show-behind-gradient="true"
          :enable-tilt="!isMobile"
          @contact-click="handleContactClick"
          class="cursor-target"
        />
      </div>

      <!-- RIGHT: TEXT -->
      <div class="text-left md:text-left">
        <h2 class="text-xl md:text-2xl font-semibold mb-4 ">Siapa Saya?</h2>

        <div class="cursor-target">
        <p class="text-gray-400 mb-4 leading-relaxed text-sm md:text-normal">
          Saya memiliki ketertarikan di bidang teknologi, khususnya dalam 
          pembuatan website yang modern dan mudah digunakan. 
          Saya senang mempelajari bagaimana sebuah tampilan web bisa dibuat menarik, 
          interaktif, dan nyaman dilihat oleh pengguna.
        </p>

        <p class="text-gray-400 mb-6 leading-relaxed text-sm md:text-normal">
           Saat ini saya sedang mengembangkan kemampuan di bidang pengembangan 
           website (frontend development) dan terus mencoba membuat berbagai 
           proyek sederhana untuk menambah pengalaman serta memahami 
           cara kerja dunia industri digital.
        </p>
</div>
        <!-- Skills -->
        <div
          class="flex flex-wrap justify-start md:justify-start gap-2 md:gap-3 mb-6"
        >
          <span
            class="bg-blue-500/20 text-blue-400 px-3 py-1 rounded-full text-xs md:text-sm"
          >
            &lt;1 Tahun Pengalaman
          </span>
          <span
            class="bg-green-500/20 text-green-400 px-3 py-1 rounded-full text-xs md:text-sm"
          >
            Desain
          </span>
          <span
            class="bg-yellow-500/20 text-yellow-400 px-3 py-1 rounded-full text-xs md:text-sm"
          >
            Coding
          </span>
          <span
            class="bg-purple-500/20 text-purple-400 px-3 py-1 rounded-full text-xs md:text-sm"
          >
            Lulusan SMK
          </span>
        </div>

        <!-- BUTTON -->
        <button
          class="button-gradient px-5 md:px-6 py-2.5 md:py-3 rounded-lg text-sm md:text-base font-semibold transition cursor-target">
          Download CV
        </button>
      </div>
    </div>
  </section>
</template>
