<script setup>
import { onMounted, provide, ref } from "vue"
import { RouterLink, RouterView } from 'vue-router'
import io from "socket.io-client";

const PORT = 3000;

// const socket = io.connect(`http://localhost:${PORT}`);
const socket = io.connect("https://concertlightsyncsystem.onrender.com:3000");

const lightColor = ref("blue")

const msg = "test message"

</script>

<template>
  <RouterView :socket="socket"/>
</template>

<style scoped>

/* レスポンシブ */
@media (min-width: 1024px) {
}
</style>
