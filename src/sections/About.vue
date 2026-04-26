<script setup lang="ts">
import { ref, onMounted } from "vue";
import ProfileCard from "../components/common/ProfileCard.vue";
import profile from "../assets/images/profile.webp";
import pattern from "../assets/images/iconpattern.webp";
import grain from "../assets/images/grain.webp";

const handleContactClick = () => {
  console.log("Contact button clicked!");
};

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
</script>

<template>
  <section
    ref="sectionRef"
    id="about"
    class="text-white py-14 md:py-20 px-6 font-poppins transition-all duration-700 will-change-transform"
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
          title="Frontend Developer"
          handle="bayu_a"
          status="Online"
          contact-text="Hubungi Saya"
          :avatar-url="profile"
          :icon-url="pattern"
          :grain-url="grain"
          :show-user-info="true"
          :show-behind-gradient="true"
          :enable-tilt="!isMobile"
          @contact-click="handleContactClick"
        />
      </div>

      <!-- RIGHT: TEXT -->
      <div class="text-left md:text-left">
        <h2 class="text-xl md:text-2xl font-semibold mb-4">Siapa Saya?</h2>

        <p class="text-gray-400 mb-4 leading-relaxed text-sm md:text-base">
          Saya adalah seorang developer yang memiliki minat besar dalam
          pengembangan website modern, khususnya menggunakan Vue.js dan Laravel.
          Saya suka membangun tampilan yang interaktif, responsif, dan nyaman
          digunakan.
        </p>

        <p class="text-gray-400 mb-6 leading-relaxed text-sm md:text-base">
          Saat ini saya fokus mengembangkan skill di bidang frontend development
          serta membangun berbagai project portfolio untuk meningkatkan
          pengalaman dan kesiapan di dunia industri.
        </p>

        <!-- Skills -->
        <div
          class="flex flex-wrap justify-start md:justify-start gap-2 md:gap-3 mb-6"
        >
          <span
            class="bg-blue-500/20 text-blue-400 px-3 py-1 rounded-full text-xs md:text-sm"
          >
            1+ Experience
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
            Student
          </span>
        </div>

        <!-- BUTTON -->
        <button
          @click="handleContactClick"
          class="button-gradient px-5 md:px-6 py-2.5 md:py-3 rounded-lg text-sm md:text-base font-semibold transition"
        >
          Hubungi Saya
        </button>
      </div>
    </div>
  </section>
</template>
