<template>
  <div>
    <p>{{ randomMatrix }}</p>
    <v-btn
    @click="addition">
      Сложение: +2
    </v-btn>
    <v-btn
    @click="multiplication">
      Умножение на число: *2
    </v-btn>
    <v-btn
    @click="matrixMultiplication">
      Умножение на матрицу [2, 2, 2, 2]
    </v-btn>
    <v-btn
    @click="power">
      Возведение в степень
    </v-btn>
    <v-btn
    @click="clear">
      Очистить
    </v-btn>
    <p>Нулевая матрица: {{ nullMatrix }}</p>
    <p>Единичная матрица: {{ onesMatrix }}</p>
    <v-btn
    @click="showInput = true">
      Ввести матрицу:
    </v-btn>
    <v-text-field
    v-if="showInput"
    v-model="inputValue"
    @click="inputValue = null">

    </v-text-field>
    <v-btn
    v-if="showInput"
    @click="convertInput">
      Подтвердить ввод
    </v-btn>
    <p
    v-if="showResult">
      Результат ввода: <p>{{ resultValue }}</p>
    </p>
    <p
    v-if="showResult">
      Транспонированная матрица: <p>{{ transposedResult }}</p>
    </p>
    <p
    v-if="showResult">
      Произведение элементов c четными номерами: <p v-if="showResult">{{ evenMultiply }}</p>
      <p v-if="showResult">Их количество:</p> <p v-if="showResult">{{ evenCount }}</p>
    </p>
  </div>
</template>

<script>
import { create, all } from 'mathjs'

const config = { }
const math = create(all, config)

export default {
  name: 'ParCalcLabsLab1',

  data() {
    return {
      matr: [[1, 1, 1, 1], [1, 1, 1, 1], [1, 1, 1, 1], [1, 1, 1, 1]],
      nullMatrix: math.zeros(4, 4),
      onesMatrix: math.ones(4, 4),
      randomMatrix: math.matrix([[Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100)],
      [Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100)],
      [Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100)],
      [Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100), Math.floor(1 * Math.random() * 100)]]),
      showInput: false,
      showResult: false,
      inputValue: '1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16',
      resultValue: null,
      transposedResult: null,
      evenMultiply: 1,
      evenCount: 0,
      cleared: null
    };
  },

  mounted() {
    this.cleared = this.randomMatrix
  },

  methods: {
    convertInput () {
      const arr = this.inputValue.split(', ')
      arr.forEach(el => {
        if (el % 2 === 0) {
          this.evenCount = this.evenCount + 1
          this.evenMultiply = this.evenMultiply * el
        }
      });
      const matrix = math.matrix([[arr[0], arr[1], arr[2], arr[3]], [arr[4], arr[5], arr[6], arr[7]], [arr[8], arr[9], arr[10], arr[11]], [arr[12], arr[13], arr[14], arr[15]]])
      this.resultValue = matrix
      this.transposedResult = math.transpose(matrix)
      this.showResult = true
      
    },
    addition() {
      this.randomMatrix = math.add(this.randomMatrix, 2)
    },
    multiplication() {
      this.randomMatrix = math.multiply(this.randomMatrix, 2)
    },
    matrixMultiplication() {
      const b = [2, 2, 2, 2]
      this.randomMatrix = math.multiply(this.randomMatrix, b)
    },
    power() {
      this.randomMatrix = math.multiply(this.randomMatrix, this.randomMatrix)
    },
    clear() {
      this.randomMatrix = this.cleared
    }
  },
};
</script>