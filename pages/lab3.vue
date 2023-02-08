<template>
  <div>
    <h1>Граф:</h1>
    <img src="https://sun9-79.userapi.com/impg/qCCt50jShJYP0JwNh790-fnx0CzScnIXNio92Q/8JcP7hGu1YQ.jpg?size=248x229&quality=96&sign=aa44a7794ea688ac65afce7c2dd40665&type=album">
    <p>Матрица графа:</p>
    <p>[0, 1, 0, 0, 0, 0, 1, 0, 0, 0]</p>
    <p>[0, 0, 0, 0, 0, 0, 0, 1, 0, 0]</p>
    <p>[0, 1, 0, 1, 0, 1, 1, 0, 0, 0]</p>
    <p>[0, 0, 0, 0, 1, 0, 0, 0, 0, 1]</p>
    <p>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]</p>
    <p>[1, 0, 0, 0, 0, 0, 1, 0, 0, 0]</p>
    <p>[0, 0, 0, 0, 0, 0, 0, 1, 0, 0]</p>
    <p>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]</p>
    <p>[0, 0, 0, 1, 0, 0, 0, 1, 0, 1]</p>
    <p>[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]</p>
    <v-row>
      <v-col
      cols="4">
        <p>Введите вершину i: </p>
        <v-text-field
        v-model="iValue">
        </v-text-field>
      </v-col>
      <v-col
      cols="4">
        <p>Введите вершину j:</p>
        <v-text-field
        v-model="kValue">
        </v-text-field>
      </v-col>
      <v-col
      cols="4">
        <p>Введите длину пути:</p>
        <v-text-field
          v-model="inputValue"
          @click="inputValue = null">
        </v-text-field>
      </v-col>
    </v-row>
    <v-btn
    @click="calculatePaths">
      Рассчитать
    </v-btn>
    <p>Результат:</p>
    <p style="white-space: pre;">{{ multipliedMatr }}</p>
    <p>Количество транзитных путей: {{ paths }}</p>
    <p>Полустепени исхода вершины i: {{ isSum }}</p>
    <p>Полустепени захода вершины i: {{ zaSum }}</p>
    <p>C: </p>
    <p style="white-space: pre;"> {{ cValue }}</p>
    <p>R: {{ rValue }}</p>
  </div>
</template>

<script>
import { create, all } from 'mathjs'

const config = { }
const math = create(all, config)
export default {
  name: 'ParcalcLab3',

  data() {
    return {
      inputValue: null,
      matr: [[0, 1, 0, 0, 0, 0, 1, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 1, 0, 0]
    ,[0, 1, 0, 1, 0, 1, 1, 0, 0, 0],[0, 0, 0, 0, 1, 0, 0, 0, 0, 1],
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [1, 0, 0, 0, 0, 0, 1, 0, 0, 0],
    [0, 0, 0, 0, 0, 0, 0, 1, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    [0, 0, 0, 1, 0, 0, 0, 1, 0, 1], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]],
    multipliedMatr: null,
    iValue: null,
    kValue: null,
    cValue: null,
    rValue: null,
    paths: null,
    isSum: 0,
    zaSum: 0
    };
  },

  methods: {
    calculatePaths() {
      this.isSum = 0
      this.zaSum = 0
      this.multipliedMatr = this.matr
      for (let i = 1; i < this.inputValue; i++) {
        this.multipliedMatr = math.multiply(this.multipliedMatr, this.matr)
      }
      this.matr[Number(this.iValue) - 1].forEach(el => {
        this.isSum = this.isSum + el
      })
      this.matr.forEach(ar => {
        ar.forEach((el, index) => {
          if (index === Number(this.iValue) - 1) {
            this.zaSum = this.zaSum + el
          }
        })
      })
      this.paths = this.multipliedMatr[Number(this.iValue) - 1][Number(this.kValue) - 1]
      let matrixSum = this.matr
      let bufferMatr = this.matr
      let matrSum = 0
      for (let i = 1; i < 10; i++) {
        bufferMatr = math.multiply(bufferMatr, this.matr)
        matrixSum = math.add(matrixSum, bufferMatr)
      }
      matrixSum.forEach(ar => {
        ar.forEach((el, index) => {
          if (el > 1) {
            ar[index] = 1
          }
        })
      })
      this.cValue = matrixSum
      this.matr.forEach(ar => {
        ar.forEach(el => {
          matrSum = matrSum + el
        })
      })
      this.rValue = ((matrSum * 0.5) / 9) - 1
      this.multipliedMatr = JSON.stringify(this.multipliedMatr).split('],[').join("],\r\n[")
      this.cValue = JSON.stringify(this.cValue).split('],[').join("],\r\n[")
    }
  },
};
</script>

<style lang="scss" scoped>

</style>