<script setup>
import ParallaxSection from '../ParallaxSection.vue'
import processImg from '../../assets/process.jpeg'

defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-[#C5895A]" textColor="text-[#2A3B30]">
    <div class="grid md:grid-cols-2 gap-12 items-center h-full">
        <div class="order-2 md:order-1 relative h-[50vh] w-full">
            <img :src="processImg" class="w-full h-full object-cover rounded-full border-8 border-[#F4F1EA]/20" />
        </div>

        <div class="order-1 md:order-2 text-[#F4F1EA]">
             <h2 class="text-5xl md:text-7xl font-serif mb-6">{{ data.title }}</h2>
             <p class="text-xl md:text-2xl leading-relaxed opacity-90 mb-12 font-light">{{ data.description }}</p>

             <div class="grid grid-cols-3 gap-8 border-t border-[#F4F1EA]/30 pt-8">
                <div v-for="stat in data.stats" :key="stat.label">
                    <div class="text-4xl font-serif">{{ stat.value }}</div>
                    <div class="text-xs uppercase tracking-widest opacity-70">{{ stat.label }}</div>
                </div>
             </div>
        </div>
    </div>
  </ParallaxSection>
</template>