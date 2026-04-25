<template>
  <footer class="pt-16 pb-8 px-6 border-t border-white/10">
    <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-10">
      <!-- LOGO / ABOUT -->
      <div>
        <h2 class="text-2xl font-bold text-gradient">@Bayu_A</h2>
        <p class="text-gray-400 mt-3 text-sm">
          Frontend Developer passionate about building modern, responsive, and
          interactive web applications.
        </p>
      </div>

      <!-- NAVIGATION -->
      <div>
        <h3 class="text-lg font-semibold mb-4">Navigation</h3>
        <ul class="space-y-2 text-gray-400">
          <li>
            <a href="#hero" class="hover:text-blue-400 transition">Home</a>
          </li>
          <li>
            <a href="#about" class="hover:text-blue-400 transition">About</a>
          </li>
          <li>
            <a href="#projects" class="hover:text-blue-400 transition"
              >Projects</a
            >
          </li>
          <li>
            <a href="#contact" class="hover:text-blue-400 transition"
              >Contact</a
            >
          </li>
        </ul>
      </div>

      <!-- SOCIAL -->
      <div>
        <h3 class="text-lg font-semibold mb-4">Follow Me</h3>
        <div class="flex gap-4">
          <a
            href="https://github.com/bayu841"
            target="_blank"
            class="w-10 h-10 flex items-center justify-center rounded-full -800 hover:bg-black transition"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-5 h-5"
              fill="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                d="M12 .5C5.7.5.6 5.7.6 12c0 5.1 3.3 9.4 7.9 10.9.6.1.8-.3.8-.6v-2.1c-3.2.7-3.9-1.4-3.9-1.4-.5-1.3-1.3-1.6-1.3-1.6-1-.7.1-.7.1-.7 1.1.1 1.7 1.2 1.7 1.2 1 .1.8 2.1 2.8 2.1.8 0 1.4-.1 1.8-.2.1-.7.4-1.2.7-1.5-2.5-.3-5.2-1.3-5.2-5.8 0-1.3.5-2.3 1.2-3.1-.1-.3-.5-1.5.1-3.1 0 0 1-.3 3.2 1.2a10.7 10.7 0 0 1 5.8 0C17 6.3 18 6.6 18 6.6c.6 1.6.2 2.8.1 3.1.8.8 1.2 1.8 1.2 3.1 0 4.5-2.7 5.5-5.3 5.8.4.4.8 1 .8 2v3c0 .3.2.7.8.6A10.9 10.9 0 0 0 23.4 12C23.4 5.7 18.3.5 12 .5z"
              />
            </svg>
          </a>
          <a
            href="https://www.instagram.com/ardiansya_byu/"
            target="_blank"
            class="w-10 h-10 flex items-center justify-center rounded-full -800 hover:bg-pink-600 transition"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-5 h-5"
              fill="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                d="M7 2C4.2 2 2 4.2 2 7v10c0 2.8 2.2 5 5 5h10c2.8 0 5-2.2 5-5V7c0-2.8-2.2-5-5-5H7zm10 2a1 1 0 1 1 0 2 1 1 0 0 1 0-2zM12 7a5 5 0 1 1 0 10 5 5 0 0 1 0-10z"
              />
            </svg>
          </a>
          <a
            href="https://www.linkedin.com/in/bayu-ardiansyah-95501b3a7/"
            target="_blank"
            class="w-10 h-10 flex items-center justify-center rounded-full -800 hover:bg-blue-600 transition"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-5 h-5"
              fill="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                d="M4.98 3.5C4.98 4.88 3.87 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1 4.98 2.12 4.98 3.5zM0 24h5V7H0v17zM8 7h4.8v2.3h.1c.7-1.3 2.5-2.7 5.2-2.7C22 6.6 24 9 24 13v11h-5v-9.5c0-2.3-.8-3.9-2.8-3.9-1.5 0-2.4 1-2.8 2-.1.3-.2.8-.2 1.3V24H8V7z"
              />
            </svg>
          </a>
        </div>
      </div>
    </div>

    <!-- BOTTOM -->
    <div
      class="mt-12 text-center text-gray-500 text-sm border-t border-white/10 pt-6"
    >
      © {{ new Date().getFullYear() }} Bayu_A. All rights reserved.
    </div>
  </footer>
</template>
