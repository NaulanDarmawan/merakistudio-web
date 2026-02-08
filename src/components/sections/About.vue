<script setup>
import ParallaxSection from '../ParallaxSection.vue'
defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-game-yellow" textColor="text-game-dark" :fitContent="true">

    <div class="grid md:grid-cols-2 gap-12 md:gap-20 items-center max-w-6xl mx-auto">

        <div class="text-center md:text-left space-y-6">
            <div class="inline-flex items-center gap-2 px-4 py-2 bg-white rounded-full border-2 border-game-dark shadow-[4px_4px_0_#2D1B4E]">
                <i class="fa-solid fa-clapperboard text-game-pink"></i>
                <span class="text-xs font-black uppercase tracking-widest text-game-dark">{{ data.title }}</span>
            </div>

            <h2 class="text-4xl md:text-6xl font-black text-game-dark leading-tight">
                {{ data.subtitle }}
            </h2>

            <p class="text-lg md:text-xl font-bold opacity-80 leading-relaxed text-game-dark/80 font-sans">
                {{ data.description }}
            </p>
        </div>

        <div class="grid gap-6">
            <div v-for="(feat, index) in data.features" :key="index"
                 class="group flex items-start gap-5 p-5 bg-white/50 hover:bg-white rounded-2xl border-2 border-game-dark/5 hover:border-game-dark transition-all duration-300 hover:-translate-y-1 hover:shadow-[6px_6px_0_#2D1B4E]">

                <div class="shrink-0 w-12 h-12 md:w-14 md:h-14 bg-game-dark text-white rounded-xl flex items-center justify-center text-xl md:text-2xl group-hover:scale-110 group-hover:rotate-6 transition duration-300 shadow-md">
                    <i :class="['fa-solid', feat.icon]"></i>
                </div>

                <div>
                    <h3 class="text-lg md:text-xl font-black uppercase tracking-wide text-game-dark mb-1">
                        {{ feat.title }}
                    </h3>
                    <p class="text-sm md:text-base font-bold opacity-60 leading-tight">
                        {{ feat.desc }}
                    </p>
                </div>
            </div>
        </div>

    </div>

  </ParallaxSection>
</template>