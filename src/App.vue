<script setup>
import { ref } from 'vue'
import contentData from './data/content.json'

// Components
import Hero from './components/sections/Hero.vue'
import Works from './components/sections/Works.vue'
import About from './components/sections/About.vue'

// Data State (Reaktif dari JSON)
const content = ref(contentData)
</script>

<template>
  <main class="font-sans antialiased selection:bg-[#C5895A] selection:text-white">
    <Hero :data="content.hero" class="z-10" />
    <About :data="content.about" class="z-20" />
    <Works :data="content.works" class="z-30" />

    <section class="sticky top-0 h-screen z-40 bg-[#1a261d] text-[#F4F1EA] flex items-center justify-center">
        <div class="text-center">
            <h2 class="text-[12vw] font-serif leading-none text-[#C5895A]">{{ content.contact.title }}</h2>
            <p class="mt-8 text-xl">{{ content.contact.email }}</p>
            <p class="opacity-50 mt-2">{{ content.contact.location }}</p>
        </div>
    </section>
  </main>
</template>