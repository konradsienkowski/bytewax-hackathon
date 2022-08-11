<template>
  <main class="app">
    <AppButton @click="playPause()" :isPlaying="isPlaying" />
    <AppPlayer :isPlaying="isPlaying" />
    <AppVisualizer :isPlaying="isPlaying" />
  </main>
</template>

<style lang="scss" src="@/assets/app.scss"></style>

<script setup>
// Import Composition API
import { ref } from 'vue'

// Import components
import AppButton from './components/AppButton.vue'
import AppPlayer from './components/AppPlayer.vue'
import AppVisualizer from './components/AppVisualizer.vue'

// Define variables
const isPlaying = ref(false)

// Play/pause method
const playPause = () => {
  isPlaying.value ? isPlaying.value = false : isPlaying.value = true 
}

</script>