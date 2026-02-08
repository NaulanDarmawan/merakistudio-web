<script setup>
defineProps({
  bgColor: { type: String, default: 'bg-game-light' },
  textColor: { type: String, default: 'text-game-dark' },
  roundedTop: { type: String, default: 'rounded-t-[50px] md:rounded-t-[80px]' },
  // Jika true: Tinggi otomatis sekecil mungkin (fit content)
  compact: { type: Boolean, default: false }
})
</script>

<template>
  <section
    class="sticky top-0 flex flex-col overflow-hidden transition-all duration-500 shadow-[0_-10px_40px_rgba(0,0,0,0.1)] border-t-2 border-white/30"
    :class="[
      bgColor,
      textColor,
      roundedTop,
      // PERUBAHAN UTAMA:
      // Jika compact: 'h-auto' (tinggi ikut konten) + padding sedang (py-12).
      // Jika tidak: 'h-screen' (layar penuh).
      compact ? 'h-auto py-12 md:py-16' : 'h-screen'
    ]"
  >
    <div class="container mx-auto px-6 md:px-12 relative z-10 flex flex-col justify-center"
         :class="{ 'h-full': !compact }">

      <div class="relative z-20">
          <slot />
      </div>

      <div class="absolute inset-0 z-0 pointer-events-none">
          <slot name="decorations" />
      </div>
    </div>
  </section>
</template>