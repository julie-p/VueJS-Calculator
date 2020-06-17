<template>
  <div class="calculator">

    <div class="display">
      {{ current || '0' }}
    </div>

    <div @click="clear" class="button">
      <p>C</p>
    </div>

    <div @click="sign" class="button">
      <p>+/-</p>
    </div>

    <div @click="percent" class="button">
      <p>%</p>
    </div>

    <div @click="divide" class="button operator">
      <p>÷</p>
    </div>

    <div @click="append('7')" class="button">
      <p>7</p>
    </div>

    <div @click="append('8')" class="button">
      <p>8</p>
    </div>

    <div @click="append('9')" class="button">
      <p>9</p>
    </div>

    <div @click="times" class="button operator">
      <p>x</p>
    </div>

    <div @click="append('4')" class="button">
      <p>4</p>
    </div>

    <div @click="append('5')" class="button">
      <p>5</p>
    </div>

    <div @click="append('6')" class="button">
      <p>6</p>
    </div>

    <div @click="minus" class="button operator">
      <p>-</p>
    </div>

    <div @click="append('1')" class="button">
      <p>1</p>
    </div>

    <div @click="append('2')" class="button">
      <p>2</p>
    </div>

    <div @click="append('3')" class="button">
      <p>3</p>
    </div>

    <div @click="add" class="button operator">
      <p>+</p>
    </div>

    <div @click="append('0')" class="button zero">
      <p>0</p>
    </div>

    <div @click="dot" class="button"> 
      <p>.</p>
    </div>

    <div @click="equal" class="button operator">
      <p>=</p>
    </div>

  </div>
  
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '', //valeur display == empty string
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear() {
      this.current = ''; //onclick sur clear, efface la valeur display et retour à 0
    },
    sign() { //Ajout de + ou - devant la valeur display 
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`; //Si - devant valeur display, on l'enlève, si elle n'est pas présente on l'ajoute
    },
    percent() { //Transforme la current value en float et la divise par 100
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) { //Concatenate le nombre cliqué avec la current value
      if (this.operatorClicked) { //Si on clique sur une opération, on clean le state current (empty string) au lieu d'append
        this.current = ''; 
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() { 
      if (this.current.indexOf('.') === -1) { //Si il n'y a pas de point, on rajoute
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
    width: 400px;
    margin: 0 auto;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .display {
    grid-column: 1 / 5;
    color: #eee;
    border-radius: 20px;
    width: 95%;
    margin: 0 auto;
  }

  p {
    margin-top: 1rem;
  }

  .zero {
    grid-column: 1 / 3;
  }

  .button {
  border: 0;
  border-radius: 20px;
  background: #DDD6F3;
  color: #6cacc5;
  cursor: pointer;
  float: left;
  font: inherit;
  margin: 0.25em;
  width: 2em;
  height: 2em;
  transition: all 0.5s;
  }
  
  .button:hover {
    background: #6cacc5;
    color: #fff;
    
  }
  
  .button:focus {
    outline: 0;
  }
    
  .button::after {
    animation: zoom 1s;
    animation-iteration-count: 1;
    animation-fill-mode: both; 
    content: attr(data-num);
    cursor: default;
    font-size: 100px;
    position: absolute;
      top: 1.5em;
      left: 50%;
    text-align: center;
    margin-left: -24px;
    opacity: 0;
    width: 48px;    
  }


</style>
