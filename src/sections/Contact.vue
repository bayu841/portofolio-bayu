<script setup>
import { ref, onMounted } from "vue";

const name = ref("");
const email = ref("");
const message = ref("");

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

const sendMessage = () => {
  if (!name.value || !email.value || !message.value) {
    alert("Harap isi semua field!");
    return;
  }

  alert("Pesan berhasil dikirim");
  name.value = "";
  email.value = "";
  message.value = "";
};
</script>

<template>
  <section
    id="contact"
    ref="sectionRef"
    :class="[
      'py-16 md:py-24 px-4 sm:px-6 text-gray-900 dark:text-white transition-all duration-700 transform',
      isVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10',
    ]"
  >
    <!-- TITLE -->
    <div class="text-center mb-12">
      <h2 class="text-4xl font-bold text-gradient">Contact Me</h2>
      <p class="text-gray-400 mt-2">
        Let's work together or discuss your project
      </p>
    </div>

    <!-- CONTAINER -->
    <div
      class="max-w-4xl mx-auto bg-gray-900/50 backdrop-blur-md border border-white/10 rounded-2xl p-5 sm:p-8 shadow-xl"
    >
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 md:gap-8">
        <!-- INFO -->
        <div>
          <h3 class="text-lg sm:text-xl font-semibold mb-4">Get in Touch</h3>
          <p class="text-gray-400 mb-6">
            Feel free to contact me for collaboration, freelance work, or just
            say hello 👋
          </p>

          <div class="space-y-3 text-gray-300">
            <!-- Location -->
            <div class="flex items-center gap-2">
              <svg
                class="w-5 h-5 text-gray-400"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M17.657 16.657L13.414 20.9a2 2 0 01-2.828 0l-4.243-4.243a8 8 0 1111.314 0z"
                />
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                />
              </svg>
              <p>Indonesia</p>
            </div>

            <!-- Email -->
            <div class="flex items-center gap-2">
              <svg
                class="w-5 h-5 text-gray-400"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8m-18 8h18a2 2 0 002-2V8a2 2 0 00-2-2H3a2 2 0 00-2 2v6a2 2 0 002 2z"
                />
              </svg>
              <p>bayuardiansyah206@gmail.com</p>
            </div>

            <!-- Phone -->
            <div class="flex items-center gap-2">
              <svg
                class="w-5 h-5 text-gray-400"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M3 5a2 2 0 012-2h2.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-1.43.716a11.042 11.042 0 005.516 5.516l.716-1.43a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
                />
              </svg>
              <p>0838-4614-0633</p>
            </div>
          </div>
        </div>

        <!-- FORM -->
        <div class="space-y-4">
          <input
            v-model="name"
            type="text"
            placeholder="Your Name"
            class="w-full px-4 py-3 text-sm sm:text-base rounded-lg bg-gray-800 border border-gray-700 focus:outline-none focus:border-blue-500"
          />

          <input
            v-model="email"
            type="email"
            placeholder="Your Email"
            class="w-full px-4 py-3 text-sm sm:text-base rounded-lg bg-gray-800 border border-gray-700 focus:outline-none focus:border-blue-500"
          />

          <textarea
            v-model="message"
            rows="4"
            placeholder="Your Message"
            class="w-full px-4 py-3 text-sm sm:text-base rounded-lg bg-gray-800 border border-gray-700 focus:outline-none focus:border-blue-500"
          ></textarea>

          <button
            @click="sendMessage"
            class="w-full py-3 rounded-lg button-gradient font-semibold text-sm sm:text-base"
          >
            Kirim Pesan
          </button>
        </div>
      </div>
    </div>
  </section>
</template>
