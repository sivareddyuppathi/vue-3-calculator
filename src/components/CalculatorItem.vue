<template>
  <div>
    <h2> CALCULATOR</h2>
    <div class="container">
      <div class="main"> {{ value }}</div>
      <div />
      <div class="button" @click="append('+')">+</div>
      <div class="button" @click="append('-')">-</div>
      <div class="button" @click="append('*')">*</div>
      <div class="button" @click="append('/')">/</div>
      <div class="history">
        <div v-for="(h, index) in history" :key="index">
          <div class="query" @click="reset(h.query)">{{ h.query }} </div>
          <div>= {{ h.result }}</div>
        </div>
        <div class="button clear-history" @click="clearHistory()">X</div>
      </div>
      <div class="button" @click="append('7')">7</div>
      <div class="button" @click="append('8')">8</div>
      <div class="button" @click="append('9')">9</div>
      <div class="button" @click="remove()">C</div>
      <div class="button equal" @click="calculate()">=</div>
      <div class="button" @click="append('4')">4</div>
      <div class="button" @click="append('5')">5</div>
      <div class="button" @click="append('6')">6</div>
      <div class="button" @click="append('%')">%</div>
      <div class="button" @click="append('1')">1</div>
      <div class="button" @click="append('2')">2</div>
      <div class="button" @click="append('3')">3</div>
      <div class="button" @click="append('0')">0</div>
      <div class="button" @click="clear()">AC</div>
      <div class="button" @click="append('.')">.</div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'CalculatorItem',

  data() {
    return {
      value: '',
      history: [],
      audio: ''
    }
  },
  mounted() {
    document.addEventListener('keydown', (event) => this.keyPressed(event), false);
    this.audio = new Audio(require("C:/Users/sures/Downloads/audio.mp3"))
  },
  methods: {
    keyPressed(e) {
      const key = e.key;
      if ((+key >= 0 && +key <= 9) || e.keyCode == 189 ||
        (e.shiftKey && (e.keyCode == 187 || e.keyCode === 53 || e.keyCode === 56 || e.keyCode === 191))) {
        this.value += key
        this.play()
      } else if (e.keyCode === 8) {
        this.remove()
        this.play()
      } else if (e.keyCode === 46) {
        this.clear()
        this.play()
      } else if (e.keyCode === 13) {
        this.play()
        this.calculate()
      }
    },
    clear() {
      this.value = ''
    },
    reset(val) {
      this.value = val
    },
    clearHistory() {
      this.history = []
    },
    calculate() {
      const result = eval(this.value)
      const obj = {
        query: this.value,
        result
      }
      this.history.push(obj)

      this.value = result

    },
    append(num) {
      this.value = (this.value + '' + num);
      this.play()
    },
    play() {
      this.audio.pause();
      this.audio.currentTime = 0;
      this.audio.play();
    },
    keyboard() {
      this.value = (Event.key)
    },
    remove() {
      this.value = this.value.slice(0, this.value.length - 1)
    },
    //  const remaining = this.value.substring(0, this.value.length - 1)
    //this.value = remaining

  },
  // beforeUnmount() {
  //   document.removeEventListener('keydown', this.keyPressed(event));
  // }
}

</script>
<style lang="scss">
.container {
  width: 500px;
  background-color: cornsilk;
  height: max-content;
  display: grid;
  grid-template-columns: repeat(5, 50px);
  grid-template-rows: repeat(6, 50px);
  justify-content: start;
  grid-gap: 10px;
  padding: 30px 0px 30px 30px;
}

.button {
  background: grey;
  border-radius: 15px;
  border-color: rgb(244, 218, 218);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: white;
}

.clear-history {
  padding: 2px 8px;
  border-radius: 50% !important;
  background-color: darkgray;
}

.main {
  grid-column-start: 1;
  grid-column-end: 5;
  grid-row-start: 1;
  font-size: 20px;
  border: 1px solid gray;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  /* gap: 17px; */
  padding: 5px;
  border-radius: 6px;
  width:230px;
  overflow: hidden;
  overflow-wrap: anywhere;


}

.equal {
  grid-column-start: 4;
  grid-row-start: 5;
  grid-row-end: 7;
}

.history {
  grid-column-start: 5;
  grid-row-start: 2;
  grid-row-end: 7;
  background-color: dimgray;
  width: 13rem;
  border-radius: 15px;
  border-color: rgb(244, 218, 218);
  color: white;
  display: flex;
  justify-content: end;
  align-items: end;
  padding: 1rem;
  flex-direction: column;
}
.query {
  cursor: pointer;
}
</style>
