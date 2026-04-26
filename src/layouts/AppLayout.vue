<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

import Navbar from "../components/common/Navbar.vue";
import Footer from "../components/common/Footer.vue";
import TargetCursor from "../components/common/TargetCursor.vue";

const isDesktop = ref(false);

const checkScreen = () => {
  isDesktop.value = window.innerWidth >= 1024; 
};

onMounted(() => {
  checkScreen();
  window.addEventListener("resize", checkScreen);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", checkScreen);
});
const isOpen = ref(false);

const songs = [
  { title: "Music 1", src: import.meta.env.BASE_URL + "/music/lagu1.mp3" },
  { title: "Music 2", src: import.meta.env.BASE_URL + "/music/lagu2.mp3" },
];

const currentIndex = ref(0);
const audio = ref(null);
const isPlaying = ref(false);

const togglePlayer = () => {
  isOpen.value = !isOpen.value;
};
const playPause = async () => {
  if (!audio.value) return;

  try {
    if (isPlaying.value) {
      audio.value.pause();
    } else {
      audio.value.load(); 
      await audio.value.play();
    }
    isPlaying.value = !isPlaying.value;
  } catch (err) {
    console.log("Audio error:", err);
  }
};

const nextSong = () => {
  currentIndex.value = (currentIndex.value + 1) % songs.length;
  playAfterChange();
};

const prevSong = () => {
  currentIndex.value =
    (currentIndex.value - 1 + songs.length) % songs.length;
  playAfterChange();
};

const playAfterChange = () => {
  isPlaying.value = false;

  setTimeout(async () => {
    if (audio.value) {
      try {
        audio.value.load(); 
        await audio.value.play();
        isPlaying.value = true;
      } catch (err) {
        console.log("Play error:", err);
      }
    }
  }, 150);
};
onMounted(() => {
  if (audio.value) {
    audio.value.volume = 1; 
  }
});
</script>

<template>
 <div class="relative min-h-screen bg-gray-950 text-white overflow-x-hidden">

  <!-- GLOBAL GLOW -->
  <div class="fixed inset-0 z-0 pointer-events-none">
    <div class="absolute w-[600px] h-[600px] bg-blue-500/25 blur-[120px] rounded-full top-[-150px] left-[-150px]"></div>
    <div class="absolute w-[500px] h-[500px] bg-purple-500/25 blur-[120px] rounded-full bottom-[-150px] right-[-150px]"></div>
  </div>

  <!-- CONTENT -->
  <Navbar />

  <!-- hanya bungkus area tertentu -->
   <TargetCursor
        v-if="isDesktop"
        :spin-duration="2"
        :hide-default-cursor="true"
    />
    <router-view />

  <Footer />
      <button
        @click="togglePlayer"
        class="fixed left-9 top-1/2 -translate-y-1/2 z-50
              w-12 h-12 rounded-full
              bg-blue-500 text-white shadow-lg
              flex items-center justify-center
              hover:scale-110 transition"
      >
          <i class="pi pi-headphones text-white text-xl"></i>
      </button>

      <!-- 🎧 POPUP PLAYER -->
      <Transition name="fade">
        <div
          v-if="isOpen"
          class="fixed left-9 top-1/2 -translate-y-1/2 z-50
                w-64 bg-gray-900/90 backdrop-blur
                p-4 rounded-xl shadow-xl border border-white/10"
        >
          <!-- Title -->
          <p class="text-white text-sm mb-2">
            {{ songs[currentIndex].title }}
          </p>

          <!-- Audio -->
          
          <!-- Controls -->
          <div class="flex justify-between items-center text-white mt-3">
            <button @click="prevSong">⏮</button>

            <button @click="playPause" class="text-lg">
              {{ isPlaying ? "⏸" : "▶️" }}
            </button>

            <button @click="nextSong">⏭</button>
          </div>

          <!-- Close -->
          <button
          @click="togglePlayer"
          class="absolute top-2 right-2 text-gray-400 hover:text-white"
          >
          ✖
        </button>
      </div>
    </Transition>
    <audio
      ref="audio"
      :key="currentIndex"
      :src="songs[currentIndex].src"
    ></audio>
</div>
</template>

<style scoped>
.interactive-area {
  width: 100%;
  height: 200px;
  border: 2px dashed #333;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.content {
  text-align: center;
  pointer-events: none;
  user-select: none;
}
</style>