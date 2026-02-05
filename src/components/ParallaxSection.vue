<script setup>
defineProps({
  // Default warna diubah menjadi tema gaming
  bgColor: { type: String, default: 'bg-game-light' },
  textColor: { type: String, default: 'text-game-dark' },
  // Prop baru untuk mengatur intensitas rounded corner jika perlu
  roundedTop: { type: String, default: 'rounded-t-[50px] md:rounded-t-[80px]' }
})
</script>

<template>
  <section
    class="sticky top-0 h-screen flex flex-col overflow-hidden transition-all duration-500 shadow-[0_-10px_40px_rgba(0,0,0,0.1)] border-t-2 border-white/30"
    :class="[bgColor, textColor, roundedTop]"
  >
    <div class="container mx-auto px-6 md:px-12 relative z-10 h-full flex flex-col justify-center pt-16">
      <div class="relative z-20">
          <slot />
      </div>

      <div class="absolute inset-0 z-0 pointer-events-none">
          <slot name="decorations" />
      </div>
    </div>
  </section>
</template>