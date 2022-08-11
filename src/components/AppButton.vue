<template>
  <button class="app__button" :class="{ 'app__button--pause': isPlaying, 'app__button--play': isPlaying === false }">
    <i class="bi" :class="{ 'bi-pause-fill': isPlaying, 'bi-play-fill': isPlaying === false }"></i>
  </button>
</template>

<script setup>
// Define props
defineProps({
  isPlaying: {
    type: Boolean,
    required: true
  }
})

</script>