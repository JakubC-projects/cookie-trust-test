<script setup lang="ts">
import { ref } from 'vue';


function sendResponse(response: unknown, origin: string) {
  if(window.parent === window) return;
  window.parent?.postMessage(JSON.stringify(response), origin)
}

let message = ref("hello world");

window.addEventListener("message", (event) => {
  console.log(event)
  if(typeof event.data !== "string") return;
  message.value = event.data
  const [command, payload] = event.data.split("/")
  console.log("commane:", command, payload)
  if(command === "get") {
    const res = localStorage.getItem(payload)
    console.log("result", res)
    sendResponse(res, event.origin)
  }
  else if(command === "set") {
    const [key, value] = payload.split(":")
    localStorage.setItem(key, value)
  }
}, false);
</script>

<template>
  <div>{{message}}</div>
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
