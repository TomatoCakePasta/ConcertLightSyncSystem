<script setup>
import { onMounted, ref } from "vue"

const props = defineProps({
    socket: Object
});

const lightColor = ref("blue")

const msg = "test message"

const socket = props.socket;

socket.on("changeColor", (newColorCode) => {
    lightColor.value = newColorCode;
});

</script>

<template>
  <div class="home" :style="{backgroundColor: lightColor}">
    <div class="title pt-5">
      <!-- <h1>ライブ名</h1>
      <p>Comming Soon ...</p> -->
    </div>
  </div>
</template>

<style scoped>
.home {
  height: 100vh;
}

.title {
  text-align: center;
}

/* レスポンシブ */
@media (min-width: 1024px) {
}
</style>