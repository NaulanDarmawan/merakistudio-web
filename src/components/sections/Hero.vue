<script setup>
import ParallaxSection from '../ParallaxSection.vue'
import heroImg from '../../assets/hero-colorful.jpeg'

defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-[#F4F1EA]" textColor="text-[#2A3B30]">
    <div class="grid md:grid-cols-2 gap-12 items-center h-full pt-20">
      <div class="space-y-6">
        <span class="uppercase tracking-[0.3em] text-sm text-[#A67C52] font-bold">Est. 2025 • Malang</span>
        <h1 class="text-6xl md:text-8xl font-serif leading-[0.9] text-[#2A3B30]">
          {{ data.title }}
        </h1>
        <p class="text-xl md:text-2xl text-[#5C6B60] max-w-md font-light">
          {{ data.subtitle }}
        </p>
      </div>

      <div class="relative h-[60vh] w-full hidden md:block">
        <div class="absolute inset-0 rounded-t-[100px] rounded-b-[40px] overflow-hidden border border-[#2A3B30]/10">
            <img :src="heroImg" class="w-full h-full object-cover hover:scale-105 transition duration-1000" />
        </div>
      </div>
    </div>
  </ParallaxSection>
</template>