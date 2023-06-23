<template>
<div class="calc">
  <div class="display">
    <input @keyup.enter="getResult" v-model="result" class="display__input" type="text">
  </div>
  <hr>
  <div class="buttons">
    <calc-button @click="allClear" class="orange">AC</calc-button>
    <calc-button @click="deleteChair" class="orange">x</calc-button>
    <calc-button @click="procent" class="orange">%</calc-button>
    <calc-button @click="() => getValue(button.value)" :class="button.color" v-for="button in buttons">{{ button.value }}</calc-button>
    <calc-button @click="getResult" class="orange">=</calc-button>
  </div>
</div>
</template>

<script>
import calcButton from '@/components/UI/calcButton.vue'

export default {
  name: 'App',
  data() {
    return {
      result: 0,
      buttons: [
        {value: '/', color: 'orange'},
        {value: '7', color: 'black'},
        {value: '8', color: 'black'},
        {value: '9', color: 'black'},
        {value: '*', color: 'orange'},
        {value: '4', color: 'black'},
        {value: '5', color: 'black'},
        {value: '6', color: 'black'},
        {value: '-', color: 'orange'},
        {value: '1', color: 'black'},
        {value: '2', color: 'black'},
        {value: '3', color: 'black'},
        {value: '+', color: 'orange'},
        {value: '0', color: 'black'},
        {value: '.', color: 'black'},
      ],
      canDelete: false,
      options: ['+','-','/','*']
    }
  },
  methods: {

    getValue(value) {
      if (+this.result === 0 && !this.options.includes(value)) {
        this.result = value
      } else if (this.options.includes(this.result[this.result.length-1]) 
                && 
                this.options.includes(value)
                || +this.result[this.result.length-1] === 0
                && +value === 0) {
        return
      } else if (this.options.includes(this.result[this.result.length-2])
                &&
                +this.result[this.result.length-1] === 0
                &&
                !this.options.includes(value)) {
        return
      } else {
        this.result += value
      }
      this.canDelete = true
    },

    getResult() {
      if (this.options.includes(this.result[this.result.length-1])) return
      this.result = eval(this.result)
      this.canDelete = false
    },

    allClear() {
      this.result = 0
    },

    deleteChair() {
      if (this.result.toString().length === 1) {
        this.result = 0;
      } else if (this.canDelete) {
        this.result = this.result.slice(0,this.result.length -1)
      }
    },

    procent() {
      if (this.options.some(el => this.result.toString().includes(el))) return
      this.result/=100
      this.canDelete = false
    }

  },
  components: {
    calcButton
  },
}
</script>

<style lang="scss">
*{
	padding: 0;
	margin: 0;
	border: 0;
}
*,*:before,*:after{
	-moz-box-sizing: border-box;
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}
:focus,:active{outline: none;}
input::-ms-clear{display: none;}
button{cursor: pointer;}
button::-moz-focus-inner {padding:0;border:0;}
a, a:visited{text-decoration: none;}
a:hover{text-decoration: none;}
ul li{list-style: none;}
img{vertical-align: top;}
h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight: 400;}
body {
  font-family: Arial, Helvetica, sans-serif;
  background-color: rgb(43, 43, 43);
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  overflow-y: scroll;
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
    &__input {
      text-align: end;
      font-size: 20px;
      font-family: Arial, Helvetica, sans-serif;
    }
  }
  .buttons {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-template-rows: repeat(5,1fr);
    align-items: center;
    justify-items: center;
    font-size: 18px;
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
