<script setup>
import CalculatorScreen from "@/components/CalculatorScreen.vue";
import CalculatorKeyBoard from "@/components/CalculatorKeyBoard.vue";
import { ref } from "vue";
const textTwo = ref("");
const text = ref("");
const fontSize = ref("");
const fontSizeSmall = ref("");
function outputSmall(output) {
  outputSmallFontSize(output);
  text.value = output;
}
function outputMain(output) {
  outputMainFontSize(output);
  if (output !== "") {
    textTwo.value = setSpase(output);
  } else {
    textTwo.value = output;
  }
}
const outputMainFontSize = (output) => {
  if (output.length > 14) {
    fontSize.value = "20";
  } else if (output.length > 10) {
    fontSize.value = "25";
  } else if (output.length > 8) {
    fontSize.value = "30";
  } else {
    fontSize.value = "40";
  }
};
const outputSmallFontSize = (output) => {
  if (output.length > 14) {
    fontSize.value = "20";
  } else if (output.length > 10) {
    fontSize.value = "25";
  } else if (output.length > 8) {
    fontSize.value = "30";
  } else {
    fontSize.value = "40";
  }
};

const setSpase = (str) => {
  if (!str.toString().includes(".")) {
    return new Intl.NumberFormat("ru-RU").format(str);
  }
  return str;
};
</script>

<template>
  <div class="calculator-frame">
    <div class="calculator-frame-main">
      <CalculatorScreen
        :text="text"
        :textTwo="textTwo"
        :fontSize="fontSize"
        :fontSizeSmall="fontSizeSmall"
      />
      <CalculatorKeyBoard @outputMain="outputMain" @outputSmall="outputSmall" />
    </div>
  </div>
</template>
<style scoped>
.calculator-frame {
  z-index: -2;
}
.calculator-frame-main {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 520px;
  width: 300px;
  z-index: -4;
  background: #f7c1ff;
  border-radius: 10px;
  border-width: 3px 3px 2px 2px;
  border-style: solid;
  border-color: #000;
}
.calculator-frame::after {
  content: "";
  z-index: -5;
  height: 520px;
  width: 300px;
  position: absolute;
  top: 2%;
  right: 3%;
  background: #e5b0ec;
  border-radius: 10px;
  border-width: 2px 2px 3px 3px;
  border-style: solid;
  border-color: #000;
}
</style>
