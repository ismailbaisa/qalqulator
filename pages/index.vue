<template>
  <div class="container">
    <el-card class="box-card">
       <h1 style="margin-bottom: 2vh;">Qalqulator</h1>
      <div class="calculator">
        <div class="answer">
          <el-row>
            <div class="current">
              <el-card style="height: 6vh">
             <b> {{ current }} </b>
              </el-card>
            </div>
          </el-row>
        </div>
        <el-row :gutter="20">
          <el-col :span="6">
            <el-button @click="clear" type="info">C</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="sign" type="warning">+/-</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="percent" type="warning">%</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="divide" type="warning">/</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('7')" type="primary">7</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('8')" type="primary">8</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('9')" type="primary">9</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="times" type="warning">x</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('4')" type="primary">4</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('5')" type="primary">5</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('6')" type="primary">6</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="minus" type="warning">-</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('1')" type="primary">1</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('2')" type="primary">2</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="append('3')" type="primary">3</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="add" type="warning">+</el-button>
          </el-col>

          <el-col :span="12">
            <el-button @click="append('0')" type="primary">0</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="dot" type="primary">.</el-button>
          </el-col>
          <el-col :span="6">
            <el-button @click="equal" type="danger">=</el-button>
          </el-col>

        </el-row>
      </div>
    </el-card>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        previous: null,
        current: '',
        operator: null,
        operatorClicked: false,
      }
    },
    methods: {
      clear() {
        this.current = '';
        this.previous = '';
      },
      sign() {
        this.current = this.current.charAt(0) === '-' ?
          this.current.slice(1) : `-${this.current}`;
      },
      percent() {
        this.current = `${parseFloat(this.current) / 100}`
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
          this.append('.')
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
          )}`
        this.previous = null;
      }
    }
  }
</script>

<style>
  .container {
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    font-weight: bold;
  }

  .el-col {
    margin-bottom: 20px;
  }

  body{
    background-color: #FFF5BA;
    font-weight: bold;
  }

  .box-card {
    width: 480px;
    background: seashell;
  }

  .el-button {
    width: 100%;
    font-weight: bold;
  }

  .answer {
    height: 10vh;
    margin-bottom: 5vh;
    margin: auto;
  }

</style>