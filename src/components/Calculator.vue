<template>
  <div class="calculator">
    <!-- DITO MAG OUTPUT AND NUMBERS -->
    <div class="display">{{current || '0'}}</div>

    <!-- PARA MABURA SA DISPLAY UNG NUMBER -->
    <div @click="clear" class="btn">C</div>

    <!-- PLUS/MINUS -->
    <div @click="sign" class="btn">+/-</div>

    <!-- PERCENT -->
    <div @click="percent" class="btn">%</div>

    <!-- DIVIDE -->
    <div @click="divide" class="btn operator">/</div>

    <!-- NUMBER 7 -->
    <div @click="append('7')" class="btn">7</div>

    <!-- NUMBER 8 -->
    <div @click="append('8')"  class="btn">8</div>

    <!-- NUMBER 9 -->
    <div @click="append('9')"  class="btn">9</div>

    <!-- MULTIPLE -->
    <div @click="times" class="btn operator">x</div>

    <!-- NUMBER 4 -->
    <div @click="append('4')" class="btn">4</div>

    <!-- NUMBER 5 -->
    <div @click="append('5')" class="btn">5</div>

    <!-- NUMBER 6 -->
    <div @click="append('6')" class="btn">6</div>

    <!-- SUBTRACT -->
    <div @click="minus" class="btn operator">-</div>

    <!-- NUMBER 1 -->
    <div @click="append('1')" class="btn">1</div>

    <!-- NUMBER 2 -->
    <div @click="append('2')" class="btn">2</div>

    <!-- NUMBER 3 -->
    <div @click="append('3')" class="btn">3</div>

    <!-- ADDITION -->
    <div @click="add" class="btn operator">+</div>

    <!-- NUMBER 0 -->
    <div @click="append('0')" class="zero btn">0</div>

    <!-- DOT -->
    <div @click="dot" class="btn">.</div>

    <!-- EQUALS -->
    <div @click="equal" class="btn operator">=</div>

  </div>
</template>

<script>
export default {
  data(){
    return{
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear(){
      this.current = ''
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ?
      this.current.slice(1) : `-${this.current}`;
    },
    percent(){
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot(){
      if(this.current.indexOf('.') === -1){
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add(){
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal(){
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator{
    width: 300px;
    margin: 0 auto;
    text-align: center;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    font-size: 40px;
  }
  .display{
    grid-column: 1 / 5;
    background-color: #333;
    text-align: end;
    padding-right: 10px;
    padding-top: 10px;
    padding-bottom: 10px;
    color: #ffffff;
  }
  .zero{
    grid-column: 1 / 3;
  }
  .btn{
    cursor: pointer;
    background-color: #f2f2f2;
    border: 1px solid #999;
  }
  .operator{
    background-color: orange;
    color: #ffffff;
  }
</style>
