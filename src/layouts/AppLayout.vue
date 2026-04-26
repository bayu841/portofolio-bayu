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