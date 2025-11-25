<template>
  <div class="max-w-[414px] w-full mx-auto h-[90vh] flex flex-col">
    <main class="flex-1 flex flex-col items-center px-6 pt-10 pb-6">
      <div class="w-full max-w-[375px] h-[30vh] mb-20 flex items-center justify-center rounded-lg">
        <img :src="images[currentIndex]" alt="Meet New People" class="max-w-full h-auto" />
      </div>

      <button
        class="w-[229px] bg-[#FF5F5F] text-white px-6 py-4 text-lg font-medium rounded-md uppercase tracking-wide mb-9"
      >
        {{ text[currentIndex] }}
      </button>

      <p class="text-[#5A5A64] leading-[1.65] text-[11px] text-center px-1 max-w-[340px]">
        It is a long established fact that a reader will be distracted by the readable content of a
        page when looking at its layout. The point of using Lorem Ipsum is that it has a
        more-or-less normal distribution of letters, as opposed to using 'Content here, Lorem Ipsum
        is that it has a more-or-less normal distribution of letters, as opposed to using 'Content
        here.
      </p>
    </main>

    <footer class="relative w-full flex items-center justify-between px-11 py-8">
      <button
        class="cursor-pointer bg-gray-100 text-[#32323C] text-xs font-semibold uppercase tracking-wide px-4 py-2 rounded"
      >
        Skip
      </button>

      <div class="absolute left-1/2 transform -translate-x-1/2 flex gap-3 items-center">
        <span
          v-for="(image, index) in images"
          :key="index"
          :class="[
            'w-2.5 h-2.5 cursor-pointer',
            currentIndex === index ? 'bg-[#FF5F5F]' : 'bg-gray-100',
          ]"
          @click="goToImage(index)"
        ></span>
      </div>

      <button
        @click="nextImage"
        class="cursor-pointer bg-[#FF5F5F] text-white text-xs font-semibold uppercase tracking-wide px-4 py-2 rounded"
      >
        Next
      </button>
    </footer>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue'
import img1 from '../img/two-phones-were-floating-two-people-came-out-of-the-phone-and-talked-directly-to-each-other-sending-heart-emoji-vector.png'
import img2 from '../img/bdfffbdc-fce8-472a-9250-b26f570ece3a.png'
import img3 from '../img/349b3421-8090-4d66-b942-92ee3bed3d05.png'

const images: string[] = [img1, img2, img3]
const text: string[] = ['Meet New People', 'CHAT WITH EASE', 'FIND YOUR MATCH']

const currentIndex = ref<number>(0)

function nextImage(): void {
  currentIndex.value = (currentIndex.value + 1) % images.length
}
function goToImage(index: number): void {
  currentIndex.value = index
}
</script>
