<template>
  <canvas class="app__visualizer" id="visualizer" 
    ref="canvas" width="1024" height="200"></canvas>
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
const canvas = ref(null)
const ws = ref(null)
const uri = 'ws://10.0.3.76:3000/'

// Draw the line based on websocket output
const drawLines = (data) => {
  const ctx = canvas.value.getContext('2d');
  ctx.clearRect(0, 0, canvas.value.width, canvas.value.height)
  ctx.strokeStyle = '#fff';
  ctx.lineWidth = 2;
  
  const data_1 = data.slice(0, 512);
  const data_2 = data.slice(512, 1024);
  data_1.reverse();
  data_2.reverse();
  const data_3 = data_1.concat(data_2);

  // Draw a line
  ctx.beginPath();
  ctx.moveTo(0, 0);

  for (let i = 0; i < data_3.length; i++) {
    ctx.lineTo(i, data_3[i]);
  }
  ctx.stroke();
}

// Start consuming the WebSocket output
const wsConnection = (state) => {
  if (state) {
    ws.value = new WebSocket(uri)
    ws.value.onmessage = (message) => {
      const data = JSON.parse(message.data)
      drawLines(data)
    }
  } else if (ws.value.readyState !== WebSocket.CLOSED){
    ws.value.close()
  }
}

// Play/pause music based on props value
watch(() => props.isPlaying, (value) => {
  if (value) wsConnection(true)
  else wsConnection(false)
})

</script>