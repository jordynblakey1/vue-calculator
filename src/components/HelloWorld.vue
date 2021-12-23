<template>
  <div class="hello">
    <div class="main-calc">
    <div class="display"> {{current || '0'}}</div>
    <div class="btn-C" @click="clear"> C </div>
    <div class="btn-neg" @click="sign()"> +/- </div>
    <div class="btn-per" @click="percent()"> % </div>
    <div class="btn-dot" @click="decimal()"> . </div>
    <div class="btn-eq" @click="operators(buttonPressed)"> = </div>
    <div class="btn-sub" @click="subtract()"> - </div>
    <div class="btn-9" @click="append(9)"> 9</div>
    <div class="btn-4" @click="append(4)"> 4 </div>
    <div class="btn-8" @click="append(8)"> 8 </div>
    <div class="btn-add" @click="add()"> + </div>
    <div class="btn-1" @click="append(1)"> 1 </div>
    <div class="btn-2" @click="append(2)"> 2 </div>
    <div class="btn-3" @click="append(3)"> 3 </div>
    <div class="btn-times" @click="mult()"> x </div>
    <div class="btn-5" @click="append(5)"> 5 </div>
    <div class="btn-6" @click="append(6)"> 6 </div>
    <div class="btn-7" @click="append(7)"> 7 </div>
    <div class="btn-div" @click="divide()"> / </div>
    <div class="btn-0" @click="append(0)"> 0 </div>
   </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '', 
      prevNum: '', 
      buttonPressed:'',
    }
  },
    methods: {
      clear() {
        this.current = ''; 
      },
      append(num) {
        //this.current +=num;
        this.current = `${this.current}${num}`
        //console.log(this.current);
      }, 
      sign() {
        //if  current is already positive make it neg, 
        //and if current is already neg make it pos
        //ternary operator returns something
         
        this.current = this.current.charAt(0) == '-' ? this.current.slice(1) : `-${this.current}`;
      },

      percent() {
        //`{}` : transforms number into a string
        this.current = `${this.current}`/100; 
      }, 
      decimal() {
        //if you press the dec. button put the decimal after current text
        this.current = this.current.charAt(0) == '0' ? this.current.concat('.') : this.current.concat('.');
        //this.current = this.current.concat('.');
      },
      add() {
        this.prevNum = this.current; 
        this.clear(); 
        this.buttonPressed = "+"; 
      }, 
      mult() {
        this.prevNum = this.current; 
        this.clear(); 
        this.buttonPressed = "*"; 
      },
       subtract() {
        this.prevNum = this.current; 
        this.clear(); 
        this.buttonPressed = "-"; 
      },
       divide() {
        this.prevNum = this.current; 
        this.clear(); 
        this.buttonPressed = "/"; 
      },
      operators(sign) {
        switch(sign) {
          case "+":
            this.current = this.buttonPressed == "+" ? parseFloat(this.current) + parseFloat(this.prevNum) : 0;
            break;
          case "-":
            this.current = this.buttonPressed == "-" ? parseFloat(this.prevNum) - parseFloat(this.current) : 0; 
            break;
          case "*":
            this.current = this.buttonPressed == "*" ? parseFloat(this.current) * parseFloat(this.prevNum) : 0; 
            break;
          case "/":
            this.current = this.buttonPressed == "/" ? parseFloat(this.prevNum) / parseFloat(this.current) : 0; 
            break;
        default:
          console.log("enter an operator");
          this.current = "ENTER AN OPERATOR"
          this.clear();
        }
      }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.main-calc {
 display: grid; 
grid-template-columns: repeat(4, 1fr); 
grid-template-rows: repeat(6, fr); 
grid-column-gap: 1px;
grid-row-gap: 1px; 
margin: 0 auto;
width: 400px;
}

.display { grid-column: 1 / 5; background-color:black; color:white;} 
.btn-C { grid-area: 2 / 1 / 3 / 2;background-color:#919191;border:solid 1px black; } 
.btn-neg { grid-area: 2 / 2 / 3 / 3; background-color:#919191;border:solid 1px black; } 
.btn-per { grid-area: 2 / 3 / 3 / 4;background-color:#919191; border:solid 1px black;} 
.btn-sub { grid-area: 2 / 4 / 3 / 5; background-color:#eda03b; border:solid 1px black;} 
.btn-9 { grid-area: 3 / 1 / 4 / 2;  background-color:#919191;border:solid 1px black;} 
.btn-4 { grid-area: 3 / 2 / 4 / 3;background-color:#919191;  border:solid 1px black;} 
.btn-8 { grid-area: 3 / 3 / 4 / 4;background-color:#919191; border:solid 1px black;} 
.btn-add { grid-area: 3 / 4 / 4 / 5;background-color:#eda03b;border:solid 1px black; } 
.btn-1 { grid-area: 4 / 1 / 5 / 2; background-color:#919191; border:solid 1px black;} 
.btn-2 { grid-area: 4 / 2 / 5 / 3;background-color:#919191; border:solid 1px black; } 
.btn-3 { grid-area: 4 / 3 / 5 / 4;background-color:#919191; border:solid 1px black; } 
.btn-times { grid-area: 4 / 4 / 5 / 5;background-color:#eda03b; border:solid 1px black; } 
.btn-5 { grid-area: 5 / 1 / 6 / 2; background-color:#919191; border:solid 1px black;} 
.btn-6 { grid-area: 5 / 2 / 6 / 3;background-color:#919191;border:solid 1px black; } 
.btn-7 { grid-area: 5 / 3 / 6 / 4;background-color:#919191;border:solid 1px black; } 
.btn-div { grid-area: 5 / 4 / 6 / 5; background-color:#eda03b; border:solid 1px black; } 
.btn-0 { grid-area: 6 / 1 / 7 / 3; background-color:yellow; border:solid 1px black;} 
.btn-dot { grid-area: 6 / 3 / 7 / 4;background-color:#919191;border:solid 1px black; } 
.btn-eq{ grid-area: 6 / 4 / 7 / 5;background-color:#eda03b;border:solid 1px black; } 
</style>
