<script setup>
import ParallaxSection from '../ParallaxSection.vue'
defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-game-yellow" textColor="text-game-dark" :autoHeight="true">

    <div class="max-w-5xl mx-auto w-full">
         <div class="flex items-center gap-4 mb-8">
            <div class="w-12 h-12 bg-game-dark rotate-45 flex items-center justify-center rounded-lg shadow-lg">
                <span class="text-2xl -rotate-45">⭐</span>
            </div>
            <h2 class="text-4xl md:text-5xl relative z-10 font-black tracking-tight">
                {{ data.title }}
            </h2>
         </div>

         <div class="grid md:grid-cols-2 gap-12 items-start">
             <div>
                 <p class="text-xl md:text-2xl font-bold leading-relaxed mb-8 text-game-dark/90 font-mono">
                    {{ data.description }}
                 </p>

                 <div class="bg-white/40 p-6 rounded-3xl border-2 border-game-dark/10 backdrop-blur-sm">
                    <p class="text-sm font-bold uppercase tracking-widest opacity-60 mb-2">Current Quest:</p>
                    <p class="text-lg font-black">Creating digital masterpieces for cool people.</p>
                 </div>
             </div>

             <div class="grid grid-cols-1 gap-4">
                <div v-for="(stat, index) in data.stats" :key="stat.label"
                     class="bg-white p-4 rounded-2xl border-b-4 border-game-dark/10 flex items-center justify-between hover:scale-105 transition-transform cursor-default group">

                    <div class="flex items-center gap-4">
                        <div class="w-12 h-12 rounded-full flex items-center justify-center text-2xl bg-game-light group-hover:bg-game-pink transition-colors">
                            <span v-if="index === 0">📂</span>
                            <span v-if="index === 1">😊</span>
                            <span v-if="index === 2">📆</span>
                        </div>
                        <div class="text-sm font-bold uppercase tracking-wider opacity-60">{{ stat.label }}</div>
                    </div>

                    <div class="text-4xl font-black text-game-purple">{{ stat.value }}</div>
                </div>
             </div>
         </div>
    </div>
  </ParallaxSection>
</template>