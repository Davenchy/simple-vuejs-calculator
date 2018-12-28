<template>
  <div class="calculaotr">
    <div class="display">{{ display }}</div>
    <div class="btn" @click="clear();">C</div>
    <div class="btn" @click="clearAll();">CA</div>
    <div class="btn" @click="negative();">-A</div>
    <div class="btn op" @click="div();">/</div>
    <div class="btn" @click="append('7');">7</div>
    <div class="btn" @click="append('8');">8</div>
    <div class="btn" @click="append('9');">9</div>
    <div class="btn op" @click="mult();">x</div>
    <div class="btn" @click="append('4');">4</div>
    <div class="btn" @click="append('5');">5</div>
    <div class="btn" @click="append('6');">6</div>
    <div class="btn op" @click="sub();">-</div>
    <div class="btn" @click="append('1');">1</div>
    <div class="btn" @click="append('2');">2</div>
    <div class="btn" @click="append('3');">3</div>
    <div class="btn op" @click="add();">+</div>
    <div class="btn zero" @click="appendZero();">0</div>
    <div class="btn" @click="appendDot();">.</div>
    <div class="btn op" @click="equal();">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: "",
      memory: null,
      solve: null
    };
  },
  methods: {
    clear() {
      this.display = "";
    },
    clearMemory() {
      this.memory = null;
      this.solve = null;
    },
    clearAll() {
      this.clear();
      this.clearMemory();
    },
    negative() {
      if (this.display.length === 0) return;
      if (this.display.indexOf("-") !== -1) return;
      this.display = `-${this.display}`;
    },
    append(text) {
      this.display += text;
    },
    appendDot() {
      if (this.display.length === 0) return this.append("0.");
      if (this.display.indexOf(".") !== -1) return;
      this.append(".");
    },
    appendZero() {
      if (this.display.length !== 0) this.append("0");
    },
    add() {
      if (this.display.length === 0) return;
      const solver = function(b) {
        this.memory += b;
      }.bind(this);
      if (this.solve === null) {
        this.memory = parseFloat(this.display);
        this.display = "";
        this.solve = solver;
      } else {
        this.solve(parseFloat(this.display));
        this.display = "";
        this.solve = solver;
      }
    },
    sub() {
      if (this.display.length === 0) return;
      const solver = function(b) {
        this.memory -= b;
      }.bind(this);
      if (this.solve === null) {
        this.memory = parseFloat(this.display);
        this.display = "";
        this.solve = solver;
      } else {
        this.solve(parseFloat(this.display));
        this.display = "";
        this.solve = solver;
      }
    },
    mult() {
      if (this.display.length === 0) return;
      const solver = function(b) {
        this.memory *= b;
      }.bind(this);
      if (this.solve === null) {
        this.memory = parseFloat(this.display);
        this.display = "";
        this.solve = solver;
      } else {
        this.solve(parseFloat(this.display));
        this.display = "";
        this.solve = solver;
      }
    },
    div() {
      if (this.display.length === 0) return;
      const solver = function(b) {
        if (b === 0) return;
        this.memory /= b;
      }.bind(this);
      if (this.solve === null) {
        this.memory = parseFloat(this.display);
        this.display = "";
        this.solve = solver;
      } else {
        this.solve(parseFloat(this.display));
        this.display = "";
        this.solve = solver;
      }
    },
    equal() {
      if (this.display.length === 0) return;
      if (this.solve === null) return;
      this.solve(parseFloat(this.display));
      this.display = this.memory;
      this.clearMemory();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="css" scoped>
.calculaotr {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: 300px;
  margin: 0 auto;
  font-size: 30px;
  border-radius: 5px;
  overflow: hidden;
}

.display {
  background-color: #222;
  color: #eee;
  grid-column: 1 / 5;
  padding: 10px;
  text-align: right;
  font-size: 40px;
}

.btn {
  cursor: pointer;
  padding: 5px;
  border: 1px solid #999;
  background-color: #eee;
  transition: opacity 0.05s;
}
.btn:active {
  box-shadow: inset 2px 0 12px #222;
}

.zero {
  grid-column: 1 / 3;
}

.op {
  background-color: orange;
  color: #f2f2f2;
}
</style>
