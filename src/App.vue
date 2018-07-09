<template>
  <div id="app">
    <img src="./assets/logo.png">
    <p>{{result}}</p>
    <div class="button-area">
      <NumberButton @onNumberClick="displayNum"/>
      <FunctionButton @onCalculate="startCalculate"/>
    </div>
    <FunctionButton v-for="test in tests" :key="test.kk" :aaa="test"></FunctionButton>
  </div>
</template>

<script>
import NumberButton from './components/NumberButton';
import FunctionButton from './components/FunctionButton';

export default {
  name: 'App',
  components: {
    NumberButton,
    FunctionButton,
  },
  data: () => ({
    result: 0,
    firstNumber: 0,
    caulateSymbol: '',
    isNumberClick: true,
    tests: [{ kk: 1, nn: 'aaa' }, { kk: 2, nn: 'bbb' }, { kk: 3, nn: 'ccc' }],
  }),
  methods: {
    displayNum(num) {
      if (num === 0 && this.result === 0) return;
      if (this.isNumberClick) {
        this.result = 0;
        this.isNumberClick = false;
      }
      this.result = (typeof this.result === 'number') ? `${num}` : this.result + num;
    },
    startCalculate(symbol) {
      if (this.result === 0) return;
      if (symbol === 'CE') {
        this.clearAll();
      } else {
        this.result = this.caulateResult(this.result, symbol);
        this.isNumberClick = true;
      }
    },
    clearAll() {
      this.result = 0;
      this.firstNumber = 0;
      this.caulateSymbol = 0;
    },
    caulateResult(num, symbol) {
      switch (symbol) {
        case '+':
          this.firstNumber += Number(num);
          break;
        case '-':
          this.firstNumber -= Number(num);
          break;
        case '*':
          this.firstNumber *= Number(num);
          break;
        case '/':
          this.firstNumber /= Number(num);
          break;
        case '=':
          this.result = this.caulateResult(num, this.caulateSymbol);
          this.firstNumber = 0;
          this.caulateSymbol = '';
          return this.result;
        default:
          this.result = 'error';
          this.clearAll();
          break;
      }
      this.caulateSymbol = symbol;
      return this.firstNumber;
    },
  },
};
</script>

<style>
.button-area{
  display: flex;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
