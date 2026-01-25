<script setup>
defineProps({
  title: String,
  category: String,
  imageSrc: String,
  color: String
})
</script>

<template>
  <div class="group relative cursor-pointer transform hover:-translate-y-2 transition-all duration-300">

    <div
      class="absolute inset-0 rounded-3xl translate-y-3 translate-x-3 transition-colors duration-300"
      :class="{
        'bg-pink-400': color === 'pink',
        'bg-blue-400': color === 'blue',
        'bg-yellow-400': color === 'yellow',
        'bg-purple-400': color === 'purple',
      }"
    ></div>

    <div class="relative bg-white rounded-3xl overflow-hidden border-4 border-black h-80 md:h-96 flex flex-col">
      <div class="h-3/4 overflow-hidden relative">
        <img
          :src="imageSrc"
          :alt="title"
          class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500 ease-out"
        />
        <div class="absolute inset-0 bg-black/0 group-hover:bg-white/20 transition-colors"></div>
      </div>

      <div class="h-1/4 bg-white p-4 flex flex-col justify-center border-t-4 border-black relative z-10">
        <span class="text-xs font-black tracking-wider uppercase mb-1"
          :class="{
            'text-pink-500': color === 'pink',
            'text-blue-500': color === 'blue',
            'text-yellow-600': color === 'yellow',
            'text-purple-500': color === 'purple',
          }"
        >{{ category }}</span>
        <h3 class="text-xl font-black text-black leading-none">{{ title }}</h3>
      </div>
    </div>
  </div>
</template>