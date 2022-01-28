<template>
  <div class="flex">
    <div class="calculator">
      <div class="input-wrap">
        <div class="smalltext" v-if="selectedOperand != ''">
          {{ prevNum }} {{ selectedOperand }} {{ selectedNum }}
        </div>
        <div class="input">{{ selectedNum }}</div>
      </div>
      <div class="button-wrap">
        <button class="clear" @click="clear('C')">C</button>
        <button class="delete" @click="delInput">del</button>
        <button class="divide" @click="keyPressed('/')">/</button>

        <button class="number" @click="keyPressed('7')">7</button>
        <button class="number" @click="keyPressed('8')">8</button>
        <button class="number" @click="keyPressed('9')">9</button>
        <button class="times" @click="keyPressed('*')">*</button>

        <button class="number" @click="keyPressed('4')">4</button>
        <button class="number" @click="keyPressed('5')">5</button>
        <button class="number" @click="keyPressed('6')">6</button>
        <button class="minus" @click="keyPressed('-')">-</button>

        <button class="number" @click="keyPressed('1')">1</button>
        <button class="number" @click="keyPressed('2')">2</button>
        <button class="number" @click="keyPressed('3')">3</button>
        <button class="plus" @click="keyPressed('+')">+</button>

        <button class="number largeno" @click="keyPressed('0')">0</button>
        <button class="result" @click="keyPressed('=')">=</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const operands = ["+", "-", "*", "/"];
    const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"];
    const selectedNum = ref("");
    const prevNum = ref("");
    const selectedOperand = ref("");

    const keyPressed = (input) => {
      if (input === "=") calculateValues();
      else if (operands.includes(input)) applyOperation(input);
      else if (numbers.includes(input)) appendNumber(input);
    };

    const clear = () => {
      selectedNum.value = "";
      prevNum.value = "";
      selectedOperand.value = "";
    };

    const delInput = () => {
      selectedNum.value = selectedNum.value.slice(0, -1);
    };

    const calculateValues = () => {
      if (selectedOperand.value === "*") multiply();

      if (selectedOperand.value === "+") sum();

      if (selectedOperand.value === "-") subtract();

      if (selectedOperand.value === "/") divide();
      prevNum.value = "";
      selectedOperand.value = "";
    };

    const appendNumber = (input) => {
      selectedNum.value = selectedNum.value + input;
    };

    const applyOperation = (input) => {
      calculateValues();
      prevNum.value = selectedNum.value;
      selectedNum.value = "";
      selectedOperand.value = input;
    };

    const multiply = () => {
      selectedNum.value = prevNum.value * selectedNum.value;
    };

    const sum = () => {
      selectedNum.value = +prevNum.value + +selectedNum.value;
    };

    const divide = () => {
      selectedNum.value = prevNum.value / selectedNum.value;
    };

    const subtract = () => {
      selectedNum.value = prevNum.value - selectedNum.value;
    };

    return {
      selectedNum,
      operands,
      numbers,
      prevNum,
      selectedOperand,
      delInput,
      calculateValues,
      applyOperation,
      clear,
      multiply,
      sum,
      divide,
      subtract,
      keyPressed,
    };
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.flex {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: rgb(63, 63, 63);
}

.calculator {
  width: 90%;
  max-width: 430px;
  padding: 25px;
  border-radius: 25px;
  background: linear-gradient(to bottom right, #524f4f, #0c0c0c);
}

/* input */
.input-wrap {
  position: relative;
  width: calc(100% - 4px);
  overflow-x: scroll;
  -ms-overflow-style: none;
  scrollbar-width: none;
  margin-bottom: 5px;
  padding: 0 5px;

  background: #a1bd66;
  text-align: right;
  box-shadow: inset 0px 0px 15px 0px rgba(0, 0, 0, 0.5);
}
.input-wrap::-webkit-scrollbar {
  display: none;
}

.input {
  height: 5rem;
  line-height: 5rem;
  font-size: 2rem;
}

.smalltext {
  position: absolute;
  right: 5px;
  top: 0.25rem;
  color: grey;
}

/* button */
.button-wrap {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  justify-content: space-around;
}

.button-wrap > button {
  width: calc(25% - 4px);
  text-align: center;
  line-height: 5rem;
  margin: 2px 0;
  background: grey;
  color: #f1f1f1;
  border-radius: 4px;
  cursor: pointer;
  user-select: none;
  outline: 0;
  transition: 0.3s;
}

.button-wrap > button.largeno {
  width: 75%;
}
.button-wrap > button.clear {
  width: 50%;
}

.button-wrap > button.number {
  background: #5d5d5f;
}

.button-wrap > button:hover {
  box-shadow: inset 0px 0px 15px 0px rgba(0, 0, 0, 0.3);
}

.button-wrap > button.result {
  background: #f55530;
}
</style>
