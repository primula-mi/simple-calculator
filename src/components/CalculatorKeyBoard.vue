<script setup>
import CalculatorButton from "@/components/CalculatorButton.vue";
import { ref } from "vue";
const output = ref("");
const emit = defineEmits(["outputMain", "outputSmall"]);
const numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
let fixedNum = 0;
let firstNum = "";
let secondNum = "";
let answer = "";
let operator = "";
const selectAction = () => {
  switch (operator) {
    case "+":
      output.value = plus();
      break;
    case "-":
      output.value = minus();
      break;
    case "×":
      output.value = multiplication();
      break;
    case "÷":
      output.value = division();
      break;
    default:
      alert("Default case");
  }
  equal();
};
const equal = () => {
  fixedNum = getFixedNum();
  emit("outputSmall", `${firstNum} ${operator} ${secondNum} = `);
  emit("outputMain", output.value.toFixed(fixedNum));
  firstNum = output.value;
  secondNum = "";
  operator = "";
  answer = output.value;
};
const plus = () => {
  return parseFloat(firstNum) + parseFloat(secondNum);
};
const minus = () => {
  return parseFloat(firstNum) - parseFloat(secondNum);
};
const multiplication = () => {
  return parseFloat(firstNum) * parseFloat(secondNum);
};
const division = () => {
  return parseFloat(firstNum) / parseFloat(secondNum);
};
const toPercentage = () => {
  if (operator === "") {
    firstNum = firstNum / 100;
    output.value = firstNum;
  } else {
    secondNum = secondNum / 100;
    output.value = secondNum;
  }
  emit("outputMain", output.value);
};
const toFloat = (event) => {
  if (operator === "") {
    firstNum += event;
  } else {
    secondNum += event;
  }
  output.value += event;
  emit("outputMain", output.value);
};
const clear = () => {
  firstNum = "";
  secondNum = "";
  operator = "";
  answer = "";
  output.value = "";
  emit("outputSmall", output.value);
  emit("outputMain", output.value);
};
const isNum = (event) => {
  if (numbers.includes(parseFloat(event))) {
    return true;
  }
  return false;
};
const enterNum = (event) => {
  if (output.value.length < 16) {
    output.value += event;
    if (operator === "") {
      firstNum += event;
    } else if (answer === "" && output.value === "") {
      secondNum = event;
    } else {
      secondNum = "";
      secondNum += output.value;
    }
    emit("outputMain", output.value);
  }
};
const getFixedNum = () => {
  let fix = 0;
  if (output.value.toString().includes(".")) {
    fixedNum = output.value
      .toString()
      .substring(output.value.toString().indexOf(".") + 1).length;
  }
  if (firstNum.toString().includes(".")) {
    fix = firstNum
      .toString()
      .substring(firstNum.toString().indexOf(".") + 1).length;
    if (fixedNum < fix) {
      fixedNum = fix;
    }
  }
  if (secondNum.toString().includes(".")) {
    fix = secondNum
      .toString()
      .substring(secondNum.toString().indexOf(".") + 1).length;
    if (fixedNum < fix) {
      fixedNum = fix;
    }
  }
  return fixedNum;
};

function clickBth(event) {
  if (event === "C") {
    clear();
  } else if (event === ".") {
    toFloat(event);
  } else if (event === "%") {
    toPercentage();
  } else if (isNum(event)) {
    enterNum(event);
  } else {
    if (secondNum !== "") {
      selectAction();
    } else {
      operator = event;
      if (answer !== "") {
        secondNum = firstNum;
      }
      answer = "";
      output.value = `${firstNum} ${event} `;
      fixedNum = getFixedNum();
      emit("outputSmall", output.value);
      emit("outputMain", firstNum.toString());
      output.value = "";
    }
  }
}
</script>
<template>
  <div class="calculator-keyboard">
    <CalculatorButton
      :class="{ 'calculator-btn--pink': true, 'g-col-2': true }"
      :text="`C`"
      @clickBth="clickBth"
    />
    <CalculatorButton
      :class="{ 'calculator-btn--pink': true }"
      :text="`%`"
      @clickBth="clickBth"
    />
    <CalculatorButton
      :class="{ 'calculator-btn--pink': true }"
      :text="`÷`"
      @clickBth="clickBth"
    />

    <CalculatorButton :text="`7`" @clickBth="clickBth" />
    <CalculatorButton :text="`8`" @clickBth="clickBth" />
    <CalculatorButton :text="`9`" @clickBth="clickBth" />
    <CalculatorButton
      :class="{ 'calculator-btn--pink': true }"
      :text="`×`"
      @clickBth="clickBth"
    />

    <CalculatorButton :text="`4`" @clickBth="clickBth" />
    <CalculatorButton :text="`5`" @clickBth="clickBth" />
    <CalculatorButton :text="`6`" @clickBth="clickBth" />
    <CalculatorButton
      :class="{ 'calculator-btn--pink': true }"
      :text="`-`"
      @clickBth="clickBth"
    />

    <CalculatorButton :text="`1`" @clickBth="clickBth" />
    <CalculatorButton :text="`2`" @clickBth="clickBth" />
    <CalculatorButton :text="`3`" @clickBth="clickBth" />
    <CalculatorButton
      :class="{ 'calculator-btn--pink': true, 'g-row-2': true }"
      :text="`+`"
      @clickBth="clickBth"
    />

    <CalculatorButton :text="`0`" @clickBth="clickBth" />
    <CalculatorButton :text="`.`" @clickBth="clickBth" />
    <CalculatorButton
      :class="{ 'calculator-btn--pink': true }"
      :text="`=`"
      @clickBth="clickBth"
    />
  </div>
</template>
<style scoped>
.calculator-keyboard {
  display: grid;
  width: 100%;
  height: 100%;
  padding: 10px 15px;
  gap: 10px;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(5, 1fr);
  user-select: none;
}
</style>
