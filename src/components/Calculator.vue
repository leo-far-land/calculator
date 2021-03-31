<template>
  <div v-on="event()">
    <span v-for="key in set" :key="key">
      <div v-if="key === ''"/>
      <b-button v-else squared variant="primary" @click="getKey(key)">{{key}}</b-button>
    </span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false,
      set: [
        "%","CE","C","⇦","",
        "1/x","x²","²√x","÷","",
        "7","8","9","X","",
        "4","5","6","-","",
        "1","2","3","+","",
        "+/-","0",",","="
      ]
    }
  },
  methods: {
    getKey(key) {
      switch(key) {
        case "CE":
        case "C":
          this.clear();
          break;
        case "-":
          this.minus();
          break;
        case "%":
          this.percent();
          break;
        case ",":
          this.dot();
          break;
        case "÷":
          this.divide();
          break;  
        case "X":
          this.times();
          break;
        case "+":
          this.add();
          break;   
        case "=":
          this.equal();
          break;  
        case "⇦":
          this.current = this.current.substr(0, this.current.length - 1);
          break;  
        case "1/x":
          this.divideForOne();
          break; 
        case "²√x":
          this.sqrt();
          break;
        case "x²":
          this.pow();
          break;
        case "+/-":
          this.times();
          break;    
        default:
          this.append(key)
          break;  
      }
    },
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
      this.current.slice(1) : `-${this.current}`;
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
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    divideForOne() {
      this.previous = this.current;
      this.current = 1;
      this.operator = (a, b) => a / b;
      this.equal();
    },
    sqrt() {
      this.current = Math.sqrt(this.current);
      this.previous = null;
    },
    pow() {
      this.current = Math.pow(this.current, 2);
      this.previous = null;
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
    event() {
      this.$emit("current", this.current);
    },
  }
}
</script>

<style>
button {
  width: 40px;
  height: 40px;
}
</style>