<script setup>
import { ref, computed } from "vue";

const display = ref("0");

const appendToDisplay = (value) => {
  if (display.value === "0" && value !== ".") {
    display.value = value;
  } else {
    display.value += value;
  }
};

const calculate = () => {
  try {
    display.value = eval(display.value).toString();
  } catch (error) {
    display.value = "Error";
  }
};


const displayClass = computed(() => {
  return display.value.length > 12 ? "small-text" : "";
});

const clearDisplay = () => {
  display.value = "0";
};
const backspace = () => {
  if (display.value !== "0") {
    display.value = display.value.slice(0, -1);
  }
};
</script>

<template>
  <div>
    <div class="calculator">
      <input v-model="display" :class="displayClass" readonly />

      <div class="buttons">
        <button @click="appendToDisplay('7')">7</button>
        <button @click="appendToDisplay('8')">8</button>
        <button @click="appendToDisplay('9')">9</button>
        <button @click="appendToDisplay('/')">/</button>

        <button @click="appendToDisplay('4')">4</button>
        <button @click="appendToDisplay('5')">5</button>
        <button @click="appendToDisplay('6')">6</button>
        <button @click="appendToDisplay('*')">*</button>

        <button @click="appendToDisplay('1')">1</button>
        <button @click="appendToDisplay('2')">2</button>
        <button @click="appendToDisplay('3')">3</button>
        <button @click="appendToDisplay('-')">-</button>

        <button @click="appendToDisplay('0')">0</button>
        <button @click="appendToDisplay('.')">.</button>
        <button @click="calculate()">=</button>
        <button @click="appendToDisplay('+')">+</button>
      </div>

      <button @click="clearDisplay" class="clear-button">C</button>
      <button @click="backspace()" class="backspace-button"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-backspace-fill" viewBox="0 0 16 16">
  <path d="M15.683 3a2 2 0 0 0-2-2h-7.08a2 2 0 0 0-1.519.698L.241 7.35a1 1 0 0 0 0 1.302l4.843 5.65A2 2 0 0 0 6.603 15h7.08a2 2 0 0 0 2-2zM5.829 5.854a.5.5 0 1 1 .707-.708l2.147 2.147 2.146-2.147a.5.5 0 1 1 .707.708L9.39 8l2.146 2.146a.5.5 0 0 1-.707.708L8.683 8.707l-2.147 2.147a.5.5 0 0 1-.707-.708L7.976 8z"/>
</svg></button>
    </div>
  </div>
</template>

<style>
input {
  padding: 10px 20px;
  margin-bottom: 20px;
  width: 85%;
}

.calculator {
  max-width: 300px;
  margin: 5% auto 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.display {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 18px;
  text-align: right;
}

.buttons {

  display: grid;
  grid-template-columns: auto auto auto auto ;
  gap: 10px;
}

button {
  background-color: rgb(0, 128, 26);
  width: 100%;
  padding: 10px;
  font-size: 18px;
}
button:hover{
    background-color: rgb(91 255 9); 
}

.clear-button {
  width: 48%;
  margin: 10px 5px  0px 0px;
}
.backspace-button {
  width: 48%;
  margin: 10px 0px  0px 5px;
}

.small-text {
  font-size: 14px;
}
</style>