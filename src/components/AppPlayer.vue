<template>
  <audio class="app__player" ref="player" loop>
    <source src="@/assets/music.wav" type="audio/wav">
  </audio>
</template>

<script setup>
// Import Composition API
import { ref, watch } from 'vue'

// Define props
const props = defineProps({
  isPlaying: {
    type: Boolean,
    required: true
  }
})

// Define variables
const player = ref(null)

// Play/pause music based on props value
watch(() => props.isPlaying, (value) => {
  if (value) player.value.play()
  else player.value.pause()
})

</script>