<script setup>
import ParallaxSection from '../ParallaxSection.vue'
defineProps(['data'])
</script>

<template>
  <ParallaxSection bgColor="bg-game-yellow" textColor="text-game-dark" :compact="true">

    <div class="max-w-6xl mx-auto w-full">

        <div class="grid md:grid-cols-12 gap-8 items-center">

            <div class="md:col-span-3 text-center md:text-left">
                <div class="inline-block px-3 py-1 bg-white border-2 border-game-dark rounded-full text-[10px] font-black uppercase tracking-widest mb-3 shadow-[2px_2px_0_#2D1B4E]">
                    {{ data.title }}
                </div>
                <h2 class="text-3xl md:text-4xl font-black text-game-dark leading-none">
                    {{ data.subtitle }}
                </h2>
            </div>

            <div class="md:col-span-5">
                <p class="text-base md:text-lg font-bold text-game-dark/80 leading-relaxed font-sans border-l-4 border-game-dark/10 pl-4 md:pl-6">
                    {{ data.description }}
                </p>
            </div>

            <div class="md:col-span-4 flex flex-col gap-3">
                <div v-for="(feat, index) in data.features" :key="index"
                     class="flex items-center gap-4 p-3 bg-white/40 rounded-xl border border-game-dark/5 hover:bg-white hover:shadow-md transition-all duration-300">

                    <div class="w-10 h-10 rounded-lg bg-game-dark text-white flex items-center justify-center text-lg shrink-0">
                        <i :class="['fa-solid', feat.icon]"></i>
                    </div>

                    <div>
                        <h4 class="text-sm font-black uppercase text-game-dark leading-none mb-0.5">
                            {{ feat.title }}
                        </h4>
                        <p class="text-xs font-bold opacity-60 leading-tight">
                            {{ feat.desc }}
                        </p>
                    </div>
                </div>
            </div>

        </div>

    </div>
  </ParallaxSection>
</template>