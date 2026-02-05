<script setup>
defineProps({
  bgColor: { type: String, default: 'bg-cream-50' },
  textColor: { type: String, default: 'text-green-900' }
})
</script>

<template>
  <section
    class="sticky top-0 h-screen flex flex-col justify-center overflow-hidden transition-colors duration-500"
    :class="[bgColor, textColor]"
  >
    <div class="container mx-auto px-6 md:px-12 relative z-10 h-full flex flex-col justify-center">
      <slot />
    </div>
  </section>
</template>