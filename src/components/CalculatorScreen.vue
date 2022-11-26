<script setup>
const props = defineProps([
  "smalltext",
  "textTwo",
  "text",
  "fontSize",
  "fontSizeSmall",
]);
</script>

<template>
  <div class="calculator-screen">
    <div class="calculator-screen-main">
      <div class="outputScreen" :style="{ fontSize: fontSizeSmall + 'px' }">
        {{ props.text }}
      </div>
      <div
        class="outputScreen outputScreen--main"
        :style="{ fontSize: fontSize + 'px' }"
      >
        {{ props.textTwo }}
      </div>
    </div>
  </div>
</template>
<style scoped>
.outputScreen {
  height: 50%;
  text-align: right;
  font-size: 20px;
  padding: 0 10px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  overflow: hidden;
}
.outputScreen--main {
  font-size: 30px;
}
.calculator-screen-main {
  height: 128px;
  width: 263px;
  margin: 30px 0 0 -10px;
  z-index: 0;
  background: #fff6ff;
  border-radius: 10px;
  border-width: 1px 1px 2px 2px;
  border-style: solid;
  border-color: #000;

  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.calculator-screen::after {
  content: "";
  z-index: -3;
  height: 137px;
  width: 273px;
  position: absolute;
  top: 21px;
  right: -10px;
  background: #e4afe9;
  border-radius: 10px;
  border-width: 2px 2px 1px 1px;
  border-style: solid;
  border-color: #000;
}
</style>
