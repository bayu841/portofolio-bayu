<script setup lang="ts">
import TiltedCard from "../components/common/TiltedCard.vue";
import { ref, onMounted } from "vue";

const texts = ["Bayu Ardiansyah", "Fresh Graduate", "Frontend Enthusiast"];

const typedText = ref("");
let textIndex = 0;
let charIndex = 0;
let isDeleting = false;

const typeSpeed = 120;
const deleteSpeed = 60;
const pauseTime = 1200;

function typeLoop() {
  const currentText = texts[textIndex];

  if (!isDeleting) {
    typedText.value = currentText.substring(0, charIndex + 1);
    charIndex++;

    if (charIndex === currentText.length) {
      isDeleting = true;
      setTimeout(typeLoop, pauseTime);
      return;
    }
  } else {
    typedText.value = currentText.substring(0, charIndex - 1);
    charIndex--;

    if (charIndex === 0) {
      isDeleting = false;
      textIndex = (textIndex + 1) % texts.length;
    }
  }

  setTimeout(typeLoop, isDeleting ? deleteSpeed : typeSpeed);
}

onMounted(() => {
  typeLoop();
});

const scrollToProjects = () => {
  const el = document.getElementById("projects");
  if (el) el.scrollIntoView({ behavior: "smooth" });
};

const scrollToContact = () => {
  const el = document.getElementById("contact");
  if (el) el.scrollIntoView({ behavior: "smooth" });
};
</script>
<template>
  <section
    class="min-h-screen flex items-center justify-center px-6 font-poppins overflow-hidden mt-4"
    id="hero"
  >
    <!-- Content -->
    <div class="max-w-6xl w-full grid md:grid-cols-2 gap-12 items-center z-10">
      <!-- LEFT TEXT -->
      <div class="ml-0 md:ml-10">
        <h1
          class="text-4xl md:text-6xl font-bold leading-tight mb-6 cursor-target"
        >
          Hi, I'm <br />
          <span class="text-gradient animate-pulse">
            {{ typedText }}
          </span>
        </h1>

        <p
          class="text-gray-400 mb-6 max-w-lg cursor-target text-sm md:text-normal"
        >
          Seorang yang memiliki minat di bidang pengembangan website, dengan
          fokus pada pembuatan tampilan yang modern, interaktif, dan responsif
        </p>

        <!-- BUTTON -->
        <div class="flex gap-3 sm:gap-4">
          <button
            @click="scrollToProjects"
            class="button-gradient px-4 py-2 sm:px-6 sm:py-3 text-sm sm:text-base rounded-lg font-semibold transition cursor-target"
          >
            Lihat Projek
          </button>

          <button
            @click="scrollToContact"
            class="border border-gray-600 hover:border-white px-4 py-2 sm:px-6 sm:py-3 text-sm sm:text-base rounded-lg transition cursor-target"
          >
            Kontak
          </button>
        </div>
      </div>

      <!-- RIGHT IMAGE / CARD -->
      <div class="justify-center hidden md:flex mt-14 rotate-[-3deg]">
        <div class="relative">
          <!-- Glow effect (tetap dipertahankan biar sama style kamu) -->
          <div class="absolute inset-0blur-3xl rounded-full"></div>

          <!-- TILTED CARD -->
          <TiltedCard
            image-src="images/heroimage.webp"
            alt-text="Bayu Profile"
            caption-text="Hi everyone💫"
            container-height="420px"
            container-width="340px"
            image-height="420px"
            image-width="340px"
            :rotate-amplitude="14"
            :scale-on-hover="1.05"
            :show-mobile-warning="false"
            :show-tooltip="true"
            :display-overlay-content="true"
            class="relative z-10 cursor-target"
          >
            <template #overlay>
              <div class="absolute bottom-4 left-4 text-white">
                <h2 class="text-lg font-bold">Bayu Ardiansyah</h2>
                <p class="text-sm text-gray-300">Frontend Developer</p>
              </div>
            </template>
          </TiltedCard>
        </div>
      </div>
    </div>
  </section>
</template>
