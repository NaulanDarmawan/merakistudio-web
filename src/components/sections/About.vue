<script setup>
import ParallaxSection from '../ParallaxSection.vue'
defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-game-yellow" textColor="text-game-dark" :autoHeight="true">

    <div class="flex justify-center w-full py-12 md:py-20">

         <div class="bg-white p-8 md:p-12 rounded-[2.5rem] shadow-[0_15px_30px_rgba(0,0,0,0.1)] text-center max-w-3xl w-full border-4 border-white ring-4 ring-game-yellow/50">

            <div class="inline-flex items-center justify-center w-16 h-16 bg-game-light text-3xl rounded-full mb-6 shadow-sm">
                👋
            </div>

            <h2 class="text-3xl md:text-5xl font-black mb-4 text-game-dark">
                {{ data.title }}
            </h2>

            <p class="text-lg md:text-xl font-bold opacity-70 mb-8 leading-relaxed">
                {{ data.description }}
            </p>

            <div class="inline-flex flex-wrap justify-center gap-4 md:gap-12 bg-game-light/50 px-8 py-4 rounded-2xl border-2 border-game-dark/5">
                <div v-for="stat in data.stats" :key="stat.label" class="text-center">
                    <div class="text-2xl md:text-3xl font-black text-game-purple">{{ stat.value }}</div>
                    <div class="text-xs uppercase tracking-widest opacity-50 font-bold">{{ stat.label }}</div>
                </div>
            </div>

         </div>

    </div>
  </ParallaxSection>
</template>