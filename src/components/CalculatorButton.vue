<script setup>
const props = defineProps({
  text: String,
});
</script>

<template>
  <div class="calculator-btn" @click="$emit('clickBth', props.text)">
    <div class="calculator-btn-main">{{ props.text }}</div>
  </div>
</template>
<style scoped>
.calculator-btn {
  grid-column: span 1;
}
.calculator-btn-main {
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  height: 100%;
  width: 100%;
  z-index: 2;
  background: #ecfffc;
  border-radius: 10px;
  border-width: 2px 2px 1px 1px;
  border-style: solid;
  border-color: #000;
  color: #000;

  font-style: normal;
  font-weight: 400;
  font-size: 32px;
  line-height: 51px;
}
.calculator-btn::after {
  content: "";
  z-index: -1;
  height: 100%;
  width: 100%;
  position: absolute;
  top: 6px;
  right: 6px;
  background: #c6dbd6;
  border-radius: 10px;
  border-width: 2px 1px 2px 2px;
  border-style: solid;
  border-color: #000;
}
.g-col-2 {
  grid-column: span 2;
}
.g-row-2 {
  grid-row: span 2;
}
.calculator-btn--pink .calculator-btn-main {
  background: #ffdfe7;
}
.calculator-btn--pink::after {
  background: #d6b2bc;
}
</style>
