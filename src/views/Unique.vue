<template>
        
    <div id="app" class="calculator">
      <div class="display">{{ display }}</div>
      <div class="buttons">
        <button v-for="button in buttons" :key="button" @click="handleButtonClick(button)">
          {{ button }}
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        display: '0',
        buttons: [
          '7', '8', '9', '÷',
          '4', '5', '6', '×',
          '1', '2', '3', '-',
          '0', '.', '=', '+',
          'C', 'DEL', '√', 'pow',
          'sin', 'cos', 'tan', 'log',
          'exp', '!', '(' ,')'
        ],
      };
    },
    methods: {
      handleButtonClick(button) {
        if (button === '=') {
          this.calculateResult();
        } else if (button === 'C') {
          this.clearDisplay();
        } else if (button === 'DEL') {
          this.deleteLastChar();
        } else {
          this.updateDisplay(button);
        }
      },
      updateDisplay(value) {
        if (this.display === '0' || this.display === 'Error') {
          this.display = value;
        } else {
          this.display += value;
        }
      },
      clearDisplay() {
        this.display = '0';
      },
      deleteLastChar() {
        if (this.display.length > 1) {
          this.display = this.display.slice(0, -1);
        } else {
          this.display = '0';
        }
      },
      calculateResult() {
        try {
          // Adding square root function
          if (this.display.includes('√')) {
            const num = parseFloat(this.display.replace('√(', '').replace(')', ''));
            this.display = Math.sqrt(num).toString();
          }
          // Adding factorial function
          else if (this.display.includes('!')) {
            const num = parseInt(this.display.slice(0, -1));
            this.display = this.factorial(num).toString();
          } else {
            this.display = eval(this.display).toString();
          }
        } catch (error) {
          this.display = 'Error';
        }
      },
      factorial(n) {
        if (n === 0 || n === 1) {
          return 1;
        } else {
          return n * this.factorial(n - 1);
        }
      },
    },
  };
  </script>
  
  <style scoped>

  .calculator {
    max-width: 400px;
    margin: 0 auto;
    border-radius: 10px;
    background-color: #f8f9fa;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    margin-top: 100px;
  }
  
  .display {
    font-size: 1.5rem;
    margin-bottom: 10px;
    padding: 10px;
    background-color: #ffffff;
    border: 1px solid #ced4da;
    border-radius: 5px;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  
  button {
    padding: 15px;
    font-size: 1.2rem;
    cursor: pointer;
    border: 1px solid #ced4da;
    border-radius: 5px;
    background-color: #e6f7ff;
    color: #0073e6;
    border: 1px solid #b3daff;
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: #f1f3f5;
  }
  </style>
  