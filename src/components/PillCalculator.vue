<template>
  <div class="page">
    <div class="shining">
      <svg class= "shine" xmlns="http://www.w3.org/2000/svg" width="127"  viewBox="0 0 77 70" fill="none">
      <path fill-rule="evenodd" clip-rule="evenodd" d="M76.4516 35.1827C56.6242 35.1675 40.3503 19.9671 38.6313 0.583008C36.9123 19.9671 20.6384 35.1675 0.811035 35.1827C20.6384 35.1978 36.9123 50.3982 38.6313 69.7823C40.3502 50.3982 56.6241 35.1978 76.4516 35.1827Z" fill="#FFC122"/>
    </svg>
      <svg class= "shine2" xmlns="http://www.w3.org/2000/svg" width="187"  viewBox="0 0 77 70" fill="none">
      <path fill-rule="evenodd" clip-rule="evenodd" d="M76.4516 35.1827C56.6242 35.1675 40.3503 19.9671 38.6313 0.583008C36.9123 19.9671 20.6384 35.1675 0.811035 35.1827C20.6384 35.1978 36.9123 50.3982 38.6313 69.7823C40.3502 50.3982 56.6241 35.1978 76.4516 35.1827Z" fill="#FFC122"/>
    </svg>
    </div>
  <div class="button-container">
    <div class="screen">{{current || '0'}}</div>
    <div @click="clear" class="button-green">AC</div>
    <div @click="sign" class="button-green">+/-</div>
    <div @click="percent" class="button-green">%</div>
    <div @click="divide" class="button-yellow">/</div>
    <div @click="append('7')" class="button-pink">7</div>
    <div @click="append('8')" class="button-pink">8</div>
    <div @click="append('9')" class="button-pink">9</div>
    <div @click="multiple" class="button-yellow">*</div>
    <div @click="append('4')" class="button-pink">4</div>
    <div @click="append('5')" class="button-pink">5</div>
    <div @click="append('6')" class="button-pink">6</div>
    <div @click="minus" class="button-yellow">-</div>
    <div @click="append('1')" class="button-pink">1</div>
    <div @click="append('2')" class="button-pink">2</div>
    <div @click="append('3')" class="button-pink">3</div>
    <div @click="add" class="button-yellow">+</div>
    <div @click="append('0')" class="zero">0</div>
    <div @click="comma" class="button-pink">,</div>
    <div @click="equal" class="button-yellow">=</div>
  </div>
  </div>
  
 
</template>

<script>
export default {
  data() {
    return {
      current: '',
      previous: null,
      operatorClicked: false,
      operator: null,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },

    sign() {
      this.current = this.current.charAt(0) === "-" ? this.current.slice(1) : `-${this.current}`;
    },
    
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },

    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
    
      if (this.current.length < 13) {
         this.current = `${this.current}${number}`;
      }
    },
    comma() {
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

    multiple() {
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


.button-container {
  display: grid;
  grid-template-rows: repeat(5, 1fr);
  grid-template-columns: repeat(4, 1fr);
  width: 440px;
  height: 430px;
  margin: auto;
  background: black;
  border-radius: 50px;
  padding-left: 20px;
  padding-top:20px;
  padding-bottom: 25px;
  font-size: 40px;
  color: black;
  font-family: monospace;
  margin-top: 120px;
  position: relative;

}

.shining {
  height: 9vh;
  position: absolute;
  top: 50px;
  left:55%; 
  z-index: 2; 
}

.shine {
  position: relative;
  left: 150px;
  top: -40px;
  animation: shineAnimation 2s infinite alternate;
  width: 90px;
}

.shine2 {
  position: relative;
  left: 57%;
  top: 60px;
  animation: shineAnimation 3s infinite alternate;
  width: 130px;
}


@keyframes shineAnimation {
  0% {
    transform: translateY(-10px);
  }
  100% {
    transform: translateY(10px);
  }
}

.button-green,
.button-yellow,
.button-pink,

.zero
{
  display: flex;
  align-items: center;
  justify-content: center;
}



.screen {
  background-color: lightblue; 
  text-align: center;
  padding: 10px;
  grid-area: 1 / span 4; 
  /* width: 500px; */
  height: 78px;
  border-radius: 50px;
  background: #3C3C3C;
  color: white;
  font-size: 65px;
  text-align: right;
  align-items: center;
  justify-content: center;
  
} 


.cell {
  background-color: #fff; 
  text-align: center;
  padding: 10px;
  border: 1px solid #ccc; 
}
.zero {
  grid-area: 6 / 1 / span 1 / span 2 ;
  background-color: #FFB5D9;
  border-radius: 42px;
}

.button-green {
   background-color: #2D8159;
   border-radius: 42px;
   height: 68px;
}

.button-yellow {
   background-color: #FFC122;
   border-radius: 42px;
   height: 68px;
}

.button-pink {
   background-color: #FFB5D9;
   border-radius: 42px;
   height: 68px;
}

.button-green:hover {
   background-color: #3E8D69; 
}

.button-yellow:hover {
   background-color: #FFD13A; 
}

.button-pink:hover, .zero:hover {
   background-color: #FFC3E3; 
}
</style>
