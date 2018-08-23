<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="b">C</div>
    <div @click="sign" class="b">+/-</div>
    <div @click="percent" class="b">%</div>
    <div @click="divide" class="b operator">÷</div>
    <div @click="append('7')" class="b">7</div>
    <div @click="append('8')" class="b">8</div>
    <div @click="append('9')" class="b">9</div>
    <div @click="times" class="b operator">x</div>
    <div @click="append('4')" class="b">4</div>
    <div @click="append('5')" class="b">5</div>
    <div @click="append('6')" class="b">6</div>
    <div @click="minus" class="b operator">-</div>
    <div @click="append('1')" class="b">1</div>
    <div @click="append('2')" class="b">2</div>
    <div @click="append('3')" class="b">3</div>
    <div @click="add" class="b operator">+</div>
    <div @click="append('0')" class="b zero">0</div>
    <div @click="dot" class="b">.</div>
    <div @click="equal" class="b operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      clickOperator: false
      }
    }, 
  methods: {
    clear() {
      this.current = ''
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current)/100}`
    }, 
    append(num){
      if (this.clickOperator) {
        this.current = '';
        this.clickOperator = false;
      }
    this.current = `${this.current}${num}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevious() {
     this.previous = this.current;
     this.clickOperator = true;
    },
    divide() {
     this.operator = (a, b) => a / b;
     this.setPrevious();
    },
    times() {
     this.operator = (a, b) => a * b;
     this.setPrevious();
    },
    minus() {
     this.operator = (a, b) => a - b;
     this.setPrevious();
    },
    add() {
     this.operator = (a, b) => a + b;
     this.setPrevious();
    },
    equal() {
     this.current = `${this.operator(
       parseFloat(this.previous), 
       parseFloat(this.current)
     )}`;
     this.previous = null;
    }
  }
}
</script>

<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }
  .display {
    grid-column: 1 / 5;
    background-color: white;
    color: #B21463;
  }
  .zero {
    grid-column: 1 / 3;
  }
  .b {
    background-color: #B21463;
    border: 1px solid white;
    border-radius: 15%;
    cursor: pointer;
  }
  .operator {
    background-color: mediumblue;
    color: white;
  }

</style>
