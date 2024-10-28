<script setup>
import { ref } from "vue"

const props = defineProps({
    socket: Object
});

// カラーパネルの配列
// TODO: DBで動的にカラーパネルの追加修正を可能にする
const colorPanel = [
  "#FF5733", // 鮮やかなオレンジ
  "#33FF57", // 鮮やかなグリーン
  "#3357FF", // 鮮やかなブルー
  "#FF33A1", // 鮮やかなピンク
  "#33FFF5", // 鮮やかなアクア
  "#F5FF33", // 鮮やかなイエロー
  "#A133FF", // 紫
  "#FF8C33", // 濃いオレンジ
  "#333FFF", // ダークブルー
  "#FF3333"  // 鮮やかなレッド
];

// 洗濯中のパネルを判別
const selectedPanelId = ref(0);

const socket = props.socket;

const onChangeLight = (idx) => {
  // 新しい色をオーディエンスに送信
  socket.emit("changeColor", colorPanel[idx])

  // 新しく選択したパネルを囲む
  selectedPanelId.value = idx
}
</script>

<template>
  <div class="home">
    <div class="title pt-5">
      <h1>ライブ名</h1>
    </div>
    <!-- リストでカラーパレット表示 -->
    <v-container>
      <v-row>
        <v-col v-for="(panel, idx) in colorPanel" :key="idx" cols="6" sm="4">
          <div 
            class="pa-2 panel"
            :class="{
              'selected': selectedPanelId === idx
            }"
          >
            <v-card
              @click="onChangeLight(idx)"
              :style="{ background: panel }"
            >
             {{ panel }} 
            </v-card>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<style scoped>
.home {
  height: 100vh;
  background-color: black;
}

.panel {
  border-radius: 4px;
}

.selected {
  outline: solid;
  outline-color: aliceblue;
}

.title {
  color: white;
  text-align: center;
}

</style>