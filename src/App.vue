<script setup>
import { ref, onMounted } from 'vue'
import GameCard from './components/GameCard.vue'

// --- ASSETS ---
import heroImg from './assets/hero-colorful.jpeg'
import game1Img from './assets/game1.jpeg'
import game2Img from './assets/game2.jpeg'
import anim1Img from './assets/anim1.jpeg' // Asset baru
import processImg from './assets/process.jpeg'
import gameplayImg from './assets/gameplay1.jpeg'

// --- STATE ---
const showVideo = ref(false)
const isScrolled = ref(false)
const activeProject = ref(null) // Kalau null berarti gak ada popup. Kalau ada isinya, popup muncul.

// Deteksi scroll
onMounted(() => {
  window.addEventListener('scroll', () => {
    isScrolled.value = window.scrollY > 50
  })
})

// FUNGSI
function toggleVideo() { showVideo.value = !showVideo.value }
function openProject(project) { activeProject.value = project } // Buka popup
function closeProject() { activeProject.value = null } // Tutup popup

// DATA
const portfolioGames = [
  {
    id: 1,
    title: "Stone Guardian",
    cat: "RPG • 2024",
    img: game1Img,
    color: "pink",
    // Data Detail untuk Popup
    desc: "Jelajahi dunia fantasi kuno di mana batu memiliki nyawa. Lawan golem raksasa, kumpulkan kristal elemen, dan selamatkan desa.",
    gallery: [gameplayImg, game1Img], // Ceritanya ini screenshot gameplay
    platform: ["Steam", "Nintendo Switch"]
  },
  {
    id: 2,
    title: "Jelly Builders",
    cat: "PUZZLE • 2023",
    img: game2Img,
    color: "yellow",
    desc: "Game puzzle fisika yang menggemaskan. Tumpuk jelly setinggi mungkin tanpa terjatuh!",
    gallery: [game2Img, gameplayImg],
    platform: ["AppStore", "PlayStore"]
  },
  {
    id: 3,
    title: "Project X",
    cat: "SECRET • 2025",
    img: game1Img,
    color: "blue",
    desc: "Project rahasia yang sedang kami kembangkan bersama publisher internasional.",
    gallery: [game1Img],
    platform: ["PC", "Console"]
  },
  {
    id: 3,
    title: "Project X",
    cat: "SECRET • 2025",
    img: game1Img,
    color: "blue",
    desc: "Project rahasia yang sedang kami kembangkan bersama publisher internasional.",
    gallery: [game1Img],
    platform: ["PC", "Console"]
  },
]

const animations = [
    { id: 1, title: "Space Candy", client: "TV Commercial", img: anim1Img },
    { id: 2, title: "Meraki Intro", client: "Branding", img: heroImg },
    { id: 3, title: "Character Reel", client: "Showcase", img: game2Img },
]
</script>

<template>
  <div class="min-h-screen bg-[#FFFDF5] text-black font-sans selection:bg-black selection:text-yellow-400 overflow-x-hidden">

    <Transition name="slide-up">
      <div v-if="activeProject" class="fixed inset-0 z-[200] flex items-end md:items-center justify-center p-0 md:p-8 bg-black/60 backdrop-blur-sm" @click.self="closeProject">

        <div class="bg-[#FFFDF5] w-full max-w-4xl h-[90vh] md:h-auto max-h-[90vh] overflow-y-auto rounded-t-3xl md:rounded-3xl shadow-2xl border-4 border-black relative flex flex-col md:flex-row">

            <button @click="closeProject" class="absolute top-4 right-4 z-20 bg-black text-white w-10 h-10 rounded-full hover:bg-red-500 transition font-bold border-2 border-white">✕</button>

            <div class="w-full md:w-1/2 bg-gray-100 border-b-4 md:border-b-0 md:border-r-4 border-black relative">
                <img :src="activeProject.img" class="w-full h-64 md:h-full object-cover" :alt="activeProject.title">
                <div class="absolute bottom-4 left-4 flex gap-2">
                    <span v-for="plat in activeProject.platform" :key="plat" class="bg-black text-white text-xs font-bold px-2 py-1 rounded shadow-lg">
                        {{ plat }}
                    </span>
                </div>
            </div>

            <div class="w-full md:w-1/2 p-8 flex flex-col">
                <span class="text-pink-600 font-black uppercase tracking-widest text-sm mb-2">{{ activeProject.cat }}</span>
                <h2 class="text-4xl font-black mb-4 leading-none">{{ activeProject.title }}</h2>
                <p class="text-gray-600 mb-6 text-lg leading-relaxed">{{ activeProject.desc }}</p>

                <div class="grid grid-cols-2 gap-4 mb-8">
                    <img v-for="(pic, idx) in activeProject.gallery" :key="idx" :src="pic" class="rounded-xl border-2 border-black hover:scale-105 transition cursor-pointer h-24 w-full object-cover">
                </div>

                <div class="mt-auto flex gap-4">
                    <button class="flex-1 bg-yellow-400 border-2 border-black py-3 font-black shadow-[4px_4px_0px_0px_rgba(0,0,0,1)] hover:translate-y-1 hover:shadow-none transition">
                        PLAY DEMO
                    </button>
                    <button class="flex-1 bg-white border-2 border-black py-3 font-bold hover:bg-gray-100 transition">
                        DETAILS
                    </button>
                </div>
            </div>
        </div>
      </div>
    </Transition>

    <Transition name="bounce">
      <div v-if="showVideo" class="fixed inset-0 z-[100] flex items-center justify-center bg-black/90 p-4 md:p-10 backdrop-blur-sm">
        <div class="relative w-full max-w-5xl bg-black border-4 border-white rounded-xl overflow-hidden shadow-[10px_10px_0px_0px_#FF00FF]">
            <button @click="toggleVideo" class="absolute top-4 right-4 z-20 bg-red-500 text-white w-10 h-10 rounded-full font-bold border-2 border-white hover:scale-110 transition">✕</button>
            <video controls autoplay class="w-full h-auto">
                <source src="./assets/hero-reel.mp4" type="video/mp4">
            </video>
        </div>
      </div>
    </Transition>

    <nav class="fixed top-0 left-0 w-full z-40 bg-[#FFFDF5] border-b-4 border-black transition-all duration-300" :class="isScrolled ? 'py-3' : 'py-5'">
      <div class="max-w-7xl mx-auto px-6 flex justify-between items-center">
        <a href="#" class="text-3xl font-black tracking-tighter flex items-center gap-2"><i class="fa-solid fa-shapes"></i> MERAKI.</a>
        <div class="hidden md:flex gap-8 font-bold text-sm uppercase tracking-wider">
          <a href="#games" class="hover:text-pink-500">Games</a>
          <a href="#animations" class="hover:text-blue-500">Animations</a>
          <a href="#process" class="hover:text-yellow-500">Process</a>
        </div>
        <button class="hidden md:block bg-black text-white px-6 py-2 font-bold border-2 border-transparent hover:shadow-[4px_4px_0px_0px_rgba(0,0,0,1)] hover:bg-white hover:text-black hover:border-black transition-all">Let's Talk</button>
      </div>
    </nav>

    <header class="pt-32 pb-20 px-6 md:px-12 border-b-4 border-black bg-grid-pattern">
        <div class="max-w-7xl mx-auto grid md:grid-cols-2 gap-12 items-center">
            <div>
                <div class="inline-block bg-pink-500 text-white px-4 py-1 font-black -rotate-2 mb-6 border-2 border-black shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]">
                    #1 CREATIVE STUDIO IN MALANG
                </div>
                <h1 class="text-6xl md:text-8xl font-black leading-none mb-8">
                    WE CRAFT <br> <span class="text-blue-600">FUN</span> & <span class="text-yellow-500">MAGIC.</span>
                </h1>
                <p class="text-xl font-medium text-gray-700 mb-8">Bukan cuma studio game. Kami adalah laboratorium imajinasi untuk Animasi, Branding, dan Digital Experience.</p>
                <div class="flex gap-4">
                    <button @click="toggleVideo" class="bg-black text-white px-8 py-4 font-bold text-lg hover:bg-gray-800 transition flex gap-2 items-center">
                        <i class="fa-solid fa-play"></i> SHOW VIDEO
                    </button>
                </div>
            </div>
            <div class="relative group cursor-pointer" @click="toggleVideo">
                <img :src="heroImg" class="w-full rounded-3xl border-4 border-black shadow-[10px_10px_0px_0px_#000] group-hover:translate-x-2 group-hover:translate-y-2 group-hover:shadow-none transition-all">
            </div>
        </div>
    </header>

    <section id="games" class="py-24 px-6 border-b-4 border-black bg-white">
        <div class="max-w-7xl mx-auto">
            <h2 class="text-5xl font-black mb-12 flex items-center gap-4">
                <i class="fa-solid fa-gamepad text-pink-500"></i> OUR GAMES
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div v-for="game in portfolioGames" :key="game.id" @click="openProject(game)">
                     <GameCard
                        :title="game.title"
                        :category="game.cat"
                        :imageSrc="game.img"
                        :color="game.color"
                     />
                </div>
            </div>
        </div>
    </section>

    <section id="animations" class="py-24 px-6 bg-yellow-50 border-b-4 border-black">
        <div class="max-w-7xl mx-auto">
            <div class="flex justify-between items-end mb-12">
                <h2 class="text-5xl font-black flex items-center gap-4">
                    <i class="fa-solid fa-film text-blue-500"></i> ANIMATIONS
                </h2>
                <p class="font-bold text-gray-500">Short Movies & Commercials</p>
            </div>

            <div class="flex gap-8 overflow-x-auto pb-8 snap-x">
                <div v-for="anim in animations" :key="anim.id" class="snap-center min-w-[300px] md:min-w-[400px] bg-white border-4 border-black p-4 rounded-xl shadow-[8px_8px_0px_0px_rgba(0,0,0,1)] hover:-translate-y-2 transition-transform cursor-pointer group">
                    <div class="h-48 overflow-hidden border-2 border-black rounded-lg mb-4 relative">
                        <img :src="anim.img" class="w-full h-full object-cover group-hover:scale-110 transition">
                        <div class="absolute inset-0 bg-black/20 flex items-center justify-center opacity-0 group-hover:opacity-100 transition">
                            <i class="fa-solid fa-play text-white text-4xl drop-shadow-lg"></i>
                        </div>
                    </div>
                    <h3 class="text-2xl font-black">{{ anim.title }}</h3>
                    <p class="text-gray-500 font-bold text-sm uppercase">{{ anim.client }}</p>
                </div>
            </div>
        </div>
    </section>

    <section id="process" class="grid md:grid-cols-2 border-b-4 border-black">
        <div class="bg-blue-600 p-12 md:p-24 flex flex-col justify-center text-white border-b-4 md:border-b-0 md:border-r-4 border-black">
            <h2 class="text-5xl md:text-7xl font-black mb-6">BEHIND <br>THE SCENE.</h2>
            <p class="text-xl font-bold mb-8 opacity-90">Kami percaya proses yang menyenangkan menghasilkan karya yang luar biasa. Intip dapur kreatif kami.</p>
            <ul class="space-y-4 text-lg font-bold">
                <li class="flex items-center gap-4"><i class="fa-solid fa-check-circle text-black"></i> Brainstorming Liar</li>
                <li class="flex items-center gap-4"><i class="fa-solid fa-check-circle text-black"></i> Sketch & Storyboard</li>
                <li class="flex items-center gap-4"><i class="fa-solid fa-check-circle text-black"></i> High-End Production</li>
            </ul>
        </div>
        <div class="h-[400px] md:h-auto relative">
            <img :src="processImg" class="w-full h-full object-cover" alt="Creative Process">
            <div class="absolute inset-0 bg-black opacity-10 bg-[url('https://www.transparenttextures.com/patterns/diagmonds-light.png')]"></div>
        </div>
    </section>

    <footer class="bg-black text-white pt-20 pb-10 text-center">
        <h2 class="text-6xl font-black text-yellow-400 mb-8">LET'S COLLAB!</h2>
        <p class="text-gray-400 mb-12">Malang, Indonesia • Est. 2025</p>
        <div class="flex justify-center gap-8 text-2xl">
            <i class="fa-brands fa-instagram hover:text-pink-500 cursor-pointer"></i>
            <i class="fa-brands fa-linkedin hover:text-blue-500 cursor-pointer"></i>
            <i class="fa-brands fa-youtube hover:text-red-500 cursor-pointer"></i>
        </div>
    </footer>

  </div>
</template>

<style>
/* Animasi Slide Up untuk Popup */
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}
.slide-up-enter-from,
.slide-up-leave-to {
  transform: translateY(100%); /* Muncul dari bawah */
  opacity: 0;
}

/* Background Pattern dot-dot kecil di hero (opsional) */
.bg-grid-pattern {
    background-image: radial-gradient(#000000 1px, transparent 1px);
    background-size: 20px 20px;
    background-color: #FFFDF5;
}
</style>