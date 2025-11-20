<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="max-w-4xl mx-auto">
      <nav class="p-4 bg-gray-100 dark:bg-gray-800 rounded-b-lg shadow-md">
        <!-- 
          RouterLink "знає" про активний маршрут.
          Ми можемо стилізувати його за допомогою 'router-link-active'
          або просто додати класи Tailwind.
        -->
        <ul class="flex gap-4">
          <li>
            <RouterLink to="/" class="text-blue-600 dark:text-blue-300 hover:underline"
              >Home</RouterLink
            >
          </li>
          <li>
            <RouterLink to="/about" class="text-blue-600 dark:text-blue-300 hover:underline"
              >About</RouterLink
            >
          </li>
          <li>
            <RouterLink to="/contact" class="text-blue-600 dark:text-blue-300 hover:underline"
              >Contact</RouterLink
            >
          </li>
        </ul>
      </nav>
    </div>
  </header>

  <main class="min-h-screen bg-white dark:bg-gray-900 text-black dark:text-white">
    <div class="max-w-4xl mx-auto mt-5">
      <RouterView />
    </div>
  </main>
</template>
