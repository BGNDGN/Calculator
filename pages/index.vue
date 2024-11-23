<template>
  <div class="Calculator">
    <textarea id="value" readonly rows="2">{{ result }}</textarea>
    <div id="buttons">
      <button class="clear" @click="clearResult">C</button>
      <button @click="appendValue('1')">1</button>
      <button @click="appendValue('2')">2</button>
      <button @click="appendValue('3')">3</button>
      <button class="operator" @click="appendValue('+')">+</button>
      <button @click="appendValue('4')">4</button>
      <button @click="appendValue('5')">5</button>
      <button @click="appendValue('6')">6</button>
      <button class="operator" @click="appendValue('-')">-</button>
      <button @click="appendValue('7')">7</button>
      <button @click="appendValue('8')">8</button>
      <button @click="appendValue('9')">9</button>
      <button class="operator" @click="appendValue('*')">*</button>
      <button @click="appendValue('0')">0</button>
      <button @click="appendValue('.')">.</button>
      <button class="equals" @click="calculateResult">=</button>
      <button class="operator" @click="appendValue('/')">/</button>
    </div>
    <p id="Title">Calculator</p>
    <p id="Powered">Powered by Burak</p>
  </div>
</template>

<script>
import './index.css';

export default {
  name: "Calculator",
  data() {
    return {
      result: "0",
    };
  },
  methods: {
    clearResult() {
      this.result = "0"; 
    },
    appendValue(value) {
      const operators = ["+", "-", "*", "/"];
      const lastChar = this.result.slice(-1);

      if (this.result === "Error") {
        this.result = operators.includes(value) ? "0" : value;
        return;
      }

      if (value === "." && this.result.includes(".")) return;
      if (operators.includes(value) && operators.includes(lastChar)) return;
      if (this.result.length >= 14) return;

      this.result = this.result === "0" ? value : this.result + value;
    },
    calculateResult() {
      try {
        const calculation = Function(`"use strict"; return (${this.result})`)();
        const calculationString = calculation.toString();

        if (calculationString.length > 14) {
          this.result = "Basamak sınırı 14'tür.";
        } else {
          this.result = calculationString;
        }
      } catch {
        this.result = "Error";
      }
    },
  },
};
</script>
