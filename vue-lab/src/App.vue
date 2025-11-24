<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <header class="h-16">
      <div class="mx-autow-full">
        <nav class="p-4 bg-white dark:bg-gray-800 border-b-2 shadow-md">
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
            <li>
              <RouterLink to="/dating-app" class="text-blue-600 dark:text-blue-300 hover:underline"
                >DatingApp</RouterLink
              >
            </li>
          </ul>
        </nav>
      </div>
    </header>
    <main class="flex-1 overflow-auto bg-white dark:bg-gray-900 text-black dark:text-white">
      <div class="max-w-4xl mx-auto p-4">
        <RouterView />
      </div>
    </main>
  </div>
</template>
