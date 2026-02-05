<script setup>
import ParallaxSection from '../ParallaxSection.vue'
import heroImg from '../../assets/hero-colorful.jpeg' // Pastikan gambar ini ceria

defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-gradient-to-b from-game-pink to-game-purple" textColor="text-white" roundedTop="rounded-t-none">

    <template #decorations>
        <div class="absolute top-20 left-10 w-20 h-20 bg-game-yellow rounded-full blur-xl opacity-50 animate-pulse"></div>
        <div class="absolute bottom-40 right-20 w-32 h-32 bg-game-blue rounded-full blur-xl opacity-40 animate-bounce delay-700"></div>
        </template>

    <div class="grid md:grid-cols-2 gap-12 items-center">
      <div class="space-y-6 text-center md:text-left">
        <span class="inline-block px-4 py-2 bg-white/20 rounded-full text-sm font-bold uppercase tracking-wider backdrop-blur-sm border-2 border-white/30">
            ✨ Level Up Your Digital World
        </span>
        <h1 class="text-5xl md:text-7xl font-extrabold drop-shadow-[0_4px_0_rgba(0,0,0,0.2)]">
          {{ data.title }}
        </h1>
        <p class="text-xl md:text-2xl opacity-90 font-bold max-w-md mx-auto md:mx-0">
          {{ data.subtitle }}
        </p>
        <button class="px-8 py-4 bg-game-yellow text-game-dark rounded-full font-black text-lg hover:scale-110 transition-transform shadow-[0_6px_0_#bda335] active:shadow-none active:translate-y-[6px]">
            {{ data.cta }}
        </button>
      </div>

      <div class="relative h-[50vh] w-full hidden md:block">
        <div class="absolute inset-0 bg-white/10 rounded-[3rem] rotate-3 backdrop-blur-sm border-4 border-white/40"></div>
        <img :src="heroImg" class="absolute inset-0 w-full h-full object-cover rounded-[3rem] hover:-rotate-2 transition duration-500 border-4 border-game-yellow shadow-xl" />
      </div>
    </div>
  </ParallaxSection>
</template>