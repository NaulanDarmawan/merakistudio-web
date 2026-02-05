<script setup>
import ParallaxSection from '../ParallaxSection.vue'
defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-game-yellow" textColor="text-game-dark">
    <div class="text-center max-w-4xl mx-auto">
         <h2 class="text-4xl md:text-6xl mb-8 relative inline-block">
            <span class="relative z-10">{{ data.title }}</span>
            <svg class="absolute -bottom-4 left-0 w-full h-6 text-game-pink/50 z-0" viewBox="0 0 100 20" preserveAspectRatio="none">
                <path d="M0,10 Q25,20 50,10 T100,10" fill="none" stroke="currentColor" stroke-width="8"/>
            </svg>
         </h2>
         <p class="text-xl md:text-2xl font-bold leading-relaxed mb-16">{{ data.description }}</p>

         <div class="grid grid-cols-3 gap-4 md:gap-8">
            <div v-for="(stat, index) in data.stats" :key="stat.label"
                 class="bg-white/50 p-6 rounded-3xl border-4 border-game-dark/10 hover:scale-105 transition shadow-sm flex flex-col items-center">
                <div class="text-4xl mb-2" v-if="index === 0">🎮</div>
                <div class="text-4xl mb-2" v-if="index === 1">💖</div>
                <div class="text-4xl mb-2" v-if="index === 2">⭐</div>

                <div class="text-4xl md:text-5xl font-black text-game-purple">{{ stat.value }}</div>
                <div class="text-sm font-bold uppercase tracking-wider opacity-70">{{ stat.label }}</div>
            </div>
         </div>
    </div>
  </ParallaxSection>
</template>