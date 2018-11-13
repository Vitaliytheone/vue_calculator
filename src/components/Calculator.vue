<template>
  <div class='calculator'>
      <div class='cell result'>{{current || '0'}}</div>
      <div @click='clear' class='cell'>AC</div>
      <div @click='sign' class='cell'>+/-</div>
      <div @click='percent' class='cell'>%</div>
      <div @click='divide' class='cell operations'>&divide;</div>
      <div @click="append('7')" class='cell'>7</div>
      <div @click="append('8')" class='cell'>8</div>
      <div @click="append('9')" class='cell'>9</div>
      <div @click='multiply' class='cell operations'>&times;</div>
      <div @click="append('4')" class='cell'>4</div>
      <div @click="append('5')" class='cell'>5</div>
      <div @click="append('6')" class='cell'>6</div>
      <div @click='minus' class='cell operations'>&#8722</div>
      <div @click="append('1')" class='cell'>1</div>
      <div @click="append('2')" class='cell'>2</div>
      <div @click="append('3')" class='cell'>3</div>
      <div @click='plus' class='cell operations'>+</div>
      <div @click="append('0')" class='cell null'>0</div>
      <div @click="dot" class='cell'>.</div>
      <div @click='equal' class='cell operations'>=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      operator: null,
      previous: null,
      operatorClicked: false,
   }
 },
 methods: {
   clear() {
       this.current = '';
   },
   sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
   },
   percent() {
     this.current = `${parseFloat(this.current) / 100}`;
   },
   append(number) {
     if (this.operatorClicked) {
       this.current = '';
       this.operatorClicked = false;
     }
     this.current = `${this.current}${number}`;
   },
   setPrevious() {
     this.previous = this.current;
     this.operatorClicked = true;
      },
   dot() {
       if (this.current.indexOf('.') === -1 && this.current !== '') {
       this.append('.');
       }
  },
  divide() {
    this.operator = (a, b) => b / a;
    this.setPrevious();
  },
  multiply() {
    this.operator = (a, b) => a * b;
    this.setPrevious();
  },
  plus() {
    this.operator = (a, b) => a + b;
    this.setPrevious();
  },
  minus() {
    this.operator = (a, b) => a - b;
    this.setPrevious();
  },
  equal() {
    if (this.previous) {
        this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`
    }
      this.previous = null;
  }
 }
}
</script>

<style scoped>
  .calculator {
    margin: 0 auto;
    width: 400px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: minmax(50px, auto);
    font-size: 30px;
    text-align: center;
  }

  .cell {
    border: 1px solid black;
    background-color: lightgrey;
  }

  .cell:hover {
    background-color: red;
    cursor: pointer;
  }
  .operations {
    background-color: orange;
    color: white;
  }

  .null {
    grid-column: 1 / 3;
  }

  .result {
    grid-column: 1 / 5;
    font-size: 50px;
    background-color: black;
    color: white;
    text-align: right;
    padding-right: 5px;
  }
</style>
