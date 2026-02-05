<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import game1 from '../../assets/game1.jpeg'
import game2 from '../../assets/game2.jpeg'
import anim1 from '../../assets/anim1.jpeg'

defineProps(['data'])
const images = { 'game1.jpeg': game1, 'game2.jpeg': game2, 'anim1.jpeg': anim1 }

// Refs
const sectionRef = ref(null)
const trackRef = ref(null)

// State
const containerHeight = ref(3000)
const translateX = ref(0)

// --- Logic Scroll (Tetap Sama karena sudah bagus) ---
const updateDimensions = () => {
    if (!trackRef.value) return
    const trackWidth = trackRef.value.scrollWidth
    const winWidth = window.innerWidth
    const scrollDistance = trackWidth - winWidth
    const finalHeight = scrollDistance > 0 ? scrollDistance + window.innerHeight : window.innerHeight
    containerHeight.value = finalHeight
}

const handleScroll = () => {
    if (!sectionRef.value || !trackRef.value) return
    const rect = sectionRef.value.getBoundingClientRect()
    const trackWidth = trackRef.value.scrollWidth
    const winWidth = window.innerWidth
    const maxTranslate = trackWidth - winWidth
    if (maxTranslate <= 0) { translateX.value = 0; return }
    const scrollProgress = -rect.top
    let x = scrollProgress
    if (x < 0) x = 0
    if (x > maxTranslate) x = maxTranslate
    translateX.value = -x
}

onMounted(async () => {
    await nextTick()
    setTimeout(() => {
        updateDimensions()
        window.addEventListener('resize', updateDimensions)
        window.addEventListener('scroll', handleScroll)
    }, 100)
})

onUnmounted(() => {
    window.removeEventListener('resize', updateDimensions)
    window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div ref="sectionRef" class="relative w-full z-30" :style="{ height: containerHeight + 'px' }">

    <div class="sticky top-0 h-screen overflow-hidden bg-[#2D1B4E] text-white flex flex-col justify-center shadow-2xl">

        <div class="absolute inset-0 z-0 opacity-20 pointer-events-none"
             style="background-image: radial-gradient(#A78BFA 1px, transparent 1px); background-size: 40px 40px;">
        </div>

        <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-[#67E8F9] rounded-full blur-[150px] opacity-20 animate-pulse"></div>
        <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-[#FF9ebb] rounded-full blur-[150px] opacity-20 animate-pulse delay-1000"></div>

        <div class="absolute top-8 left-0 w-full px-6 md:px-16 z-10 flex justify-between items-start pointer-events-none">
            <div>
                <h2 class="text-4xl md:text-6xl font-black text-transparent bg-clip-text bg-gradient-to-r from-[#67E8F9] to-[#FF9ebb] drop-shadow-sm">
                    GAME LIBRARY
                </h2>
                <div class="h-1 w-20 bg-[#FDE047] mt-2 rounded-full"></div>
            </div>
             <div class="hidden md:flex flex-col items-end gap-1">
                <span class="text-xs font-mono text-[#67E8F9]">SYSTEM_READY</span>
                <span class="text-xs font-mono text-white/50">SCROLL_TO_BROWSE</span>
            </div>
        </div>

        <div ref="trackRef" class="flex items-center gap-12 px-8 md:px-[10vw] w-max h-full pt-16"
             :style="{ transform: `translateX(${translateX}px)` }">

            <div v-for="(item, index) in data" :key="item.id" class="group relative perspective-1000">

                <div class="w-[280px] md:w-[320px] relative transition-all duration-500 group-hover:-translate-y-8 group-hover:rotate-2">

                    <div class="absolute -inset-2 bg-gradient-to-br from-white/20 to-white/5 rounded-[2.5rem] blur-sm opacity-0 group-hover:opacity-100 transition duration-500"></div>

                    <div class="relative bg-[#1a1a2e] p-3 rounded-[2rem] border border-white/10 shadow-[0_20px_40px_rgba(0,0,0,0.4)] overflow-hidden">

                        <div class="flex justify-between px-4 py-2 opacity-30">
                            <div class="w-2 h-2 rounded-full bg-white"></div>
                            <div class="w-2 h-2 rounded-full bg-white"></div>
                        </div>

                        <div class="relative h-[200px] rounded-[1.5rem] overflow-hidden border-2 border-[#2D1B4E] group-hover:border-[#67E8F9] transition-colors duration-300">
                            <img :src="images[item.image]" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 group-hover:scale-110 transition duration-700">
                            <div class="absolute inset-0 bg-[#67E8F9] mix-blend-overlay opacity-0 group-hover:opacity-20 transition"></div>
                        </div>

                        <div class="pt-4 pb-2 px-2 text-center">
                            <span class="inline-block px-3 py-1 bg-[#2D1B4E] border border-[#A78BFA] rounded-md text-[10px] font-mono text-[#A78BFA] mb-2 uppercase tracking-widest">
                                {{ item.category }}
                            </span>

                            <h3 class="text-2xl font-black text-white mb-1 leading-none">{{ item.title }}</h3>
                            <p class="text-white/50 text-xs font-sans line-clamp-2 px-2 h-8">{{ item.description }}</p>

                            <div class="mt-6 flex justify-center">
                                <button class="relative inline-flex group/btn cursor-pointer">
                                    <div class="absolute transition-all duration-200 rounded-lg -inset-px bg-gradient-to-r from-[#FDE047] to-[#FDE047] group-hover/btn:blur-lg group-hover/btn:opacity-70 opacity-0"></div>
                                    <div class="relative inline-flex items-center justify-center px-6 py-2 text-sm font-black text-[#2D1B4E] transition-all duration-200 bg-[#FDE047] font-mono rounded-lg focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-900 border-b-4 border-[#bda335] active:border-b-0 active:translate-y-1">
                                        START GAME ►
                                    </div>
                                </button>
                            </div>
                        </div>

                        <div class="flex justify-center gap-1 mt-4 mb-1 opacity-10">
                            <div class="w-1 h-3 bg-white rounded-full"></div>
                            <div class="w-1 h-3 bg-white rounded-full"></div>
                            <div class="w-1 h-3 bg-white rounded-full"></div>
                        </div>
                    </div>
                </div>

                <div class="mt-6 mx-auto w-[60%] h-2 bg-black/40 rounded-[100%] blur-md transition-all duration-500 group-hover:w-[40%] group-hover:blur-xl"></div>
            </div>

            <div class="w-[5vw] h-1 shrink-0"></div>

        </div>
    </div>
  </div>
</template>

<style scoped>
.perspective-1000 {
    perspective: 1000px;
}
/* Font Mono untuk kesan gaming */
.font-mono {
    font-family: 'Courier New', Courier, monospace;
}
</style>