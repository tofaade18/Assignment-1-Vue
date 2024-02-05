<template>
  <div class="calculator">
    <input v-model="display" readonly />
    <div class="buttons">
      <button v-for="button in buttons" :key="button.value" @click="handleButtonClick(button)">
        {{ button.label }}
      </button>
    </div>
    <div class="buttons2">
      <button v-for="button2 in buttons2" :key="button2.value" @click="handleButtonClick2(button2)">
        {{ button2.label }}
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
      { label: '7', value: '7' },
        { label: '8', value: '8' },
        { label: '9', value: '9' },
        { label: '/', value: '/', flex: '1' },
        { label: '4', value: '4',flex: '1' },
        { label: '5', value: '5' },
        { label: '6', value: '6' },
        { label: '*', value: '*', flex: '1' },
        { label: '1', value: '1' },
        { label: '2', value: '2' },
        { label: '3', value: '3' },
        { label: '-', value: '-', flex: '1' },
        { label: '0', value: '0' },
        { label: '.', value: '.' },
        { label: '+', value: '+', flex: '1' },
        { label: 'C', value: 'C', flex: '1' },
      ],
      buttons2 : [
        { label: '=', value: '='}
      ]
    };
  },
  methods: {
    handleButtonClick(button) {
      if (button.value === 'C') {
        this.clearDisplay();
      } else {
        this.updateDisplay(button.value);
      }
    },
    handleButtonClick2(button) {
    if (button.value === '=') {
        this.calculateResult();
      }
    },
    updateDisplay(value) {
      if (this.display === '0' || this.display === 'Error') {
        this.display = value;
      } else {
        this.display += value;
      }
    },
    calculateResult() {
      try {
        this.display = eval(this.display).toString();
      } catch (error) {
        this.display = 'Error';
      }
    },
    clearDisplay() {
      // Remove the last entered character
      this.display = this.display.slice(0, -1);
      // If the display becomes empty, set it to '0'
      if (this.display === '') {
        this.display = '0';
      }
    }
  },
};
</script>

<style scoped>
.calculator {
  width: 300px;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin: 0 auto;
  margin-top: 50px;
}

input {
  width: 100%;
  height: 40px;
  font-size: 20px;
  text-align: right;
  margin-bottom: 10px;
}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}
.buttons2 {
  display: grid;
  width: 100%;
  font-size: 24px;
  margin-top: 10px;
  background-color: red;
}
button {
  width: 100%;
  height: 40px;
  font-size: 18px;
  border: 1px solid #ccc;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}


button:hover {
  background-color: #e0e0e0;
}
</style>
