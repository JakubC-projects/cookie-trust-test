<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { onMounted } from 'vue';

const frameOrigin = "http://child.example.com"

let frame: HTMLIFrameElement | undefined;
onMounted(() => {
  frame = document.getElementById("frame") as HTMLIFrameElement
})
let inputVal = "";

function sendMessage() {
  if(!frame) return;
  frame.contentWindow?.postMessage(inputVal, frameOrigin)
}

window.addEventListener("message", event => {
  console.log(event.data)
})
</script>

<template>
  <input v-model="inputVal"/>
  <button @click="sendMessage">send</button>
  <iframe :src="frameOrigin" id="frame"></iframe>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
