<template>
<div class="calc">
  <div class="display">{{ value1 }}{{ sign }}{{ value2 }}</div>
  <hr>
  <div class="buttons">
    <calc-button @click="() => getValue(button)" :class="button.color" v-for="button in buttons">{{ button.value }}</calc-button>
  </div>
</div>
</template>

<script>
import calcButton from '@/components/UI/calcButton.vue'

export default {
  name: 'App',
  data() {
    return {
      value1: 0,
      value2: 0,
      sign: '+',
      buttons: [
        {value: 'AC', color: 'orange'},
        {value: 'x', color: 'orange'},
        {value: '%', color: 'orange'},
        {value: '/', color: 'orange', type: 'sign'},
        {value: '7', color: 'black'},
        {value: '8', color: 'black'},
        {value: '9', color: 'black'},
        {value: 'X', color: 'orange', type: 'sign'},
        {value: '4', color: 'black'},
        {value: '5', color: 'black'},
        {value: '6', color: 'black'},
        {value: '-', color: 'orange', type: 'sign'},
        {value: '1', color: 'black'},
        {value: '2', color: 'black'},
        {value: '3', color: 'black'},
        {value: '+', color: 'orange', type: 'sign'},
        {value: '0', color: 'black'},
        {value: ',', color: 'black'},
        {value: '=', color: 'orange'},
      ]
    }
  },

  components: {
    calcButton
  },
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  background-color: rgb(43, 43, 43);
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-size: 20px;
}
.calc {
  width: 300px;
  height: 500px;
  background-color: #fff;
  border-radius: 15px;
  padding: 10px;
  .display {
    height: 45%;
    display: flex;
    justify-content: end;
    align-items: end;
    padding: 10px 30px;
  }
  .buttons {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-template-rows: repeat(5,1fr);
    align-items: center;
    justify-items: center;
  }
  .orange {
    color: orange;
  }
  .black {
    color: black;
  }
  hr {
    display: block;
    height: 1px;
    width: 100%;
    background-color: #a7a7a7;
  }
}
</style>
