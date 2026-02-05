<script setup>
import { computed } from 'vue'
import ParallaxSection from '../ParallaxSection.vue'
// Import gambar secara manual karena Vite butuh path statis untuk optimasi
import game1 from '../../assets/game1.jpeg'
import game2 from '../../assets/game2.jpeg'
import anim1 from '../../assets/anim1.jpeg'

const props = defineProps(['data'])

// Helper sederhana untuk mapping string nama file ke import file
const images = { 'game1.jpeg': game1, 'game2.jpeg': game2, 'anim1.jpeg': anim1 }
</script>

<template>
  <ParallaxSection bgColor="bg-[#2A3B30]" textColor="text-[#F4F1EA]">
    <div class="h-full py-12 flex flex-col">
        <h2 class="text-4xl md:text-6xl font-serif mb-12 text-[#E9EDC9]">Selected Works</h2>

        <div class="flex-1 overflow-x-auto flex gap-8 pb-8 snap-x items-center">
            <div v-for="item in data" :key="item.id"
                 class="snap-center shrink-0 w-[300px] md:w-[400px] group cursor-pointer">

                <div class="relative h-[400px] rounded-[2rem] overflow-hidden mb-6 transition-transform duration-500 group-hover:-translate-y-2">
                    <img :src="images[item.image]" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 transition duration-500">
                    <div class="absolute inset-0 bg-black/20 group-hover:bg-transparent transition"></div>
                </div>

                <div class="px-2">
                    <span class="text-[#A67C52] text-xs font-bold tracking-widest uppercase mb-2 block">{{ item.category }}</span>
                    <h3 class="text-3xl font-serif leading-none mb-2">{{ item.title }}</h3>
                    <p class="text-[#F4F1EA]/60 text-sm line-clamp-2">{{ item.description }}</p>
                </div>
            </div>
        </div>
    </div>
  </ParallaxSection>
</template>