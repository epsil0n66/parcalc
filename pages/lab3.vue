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
    <p>Введите длину пути:</p>
    <v-text-field
    v-model="inputValue"
    @click="inputValue = null">
    </v-text-field>
    <v-btn
    @click="calculatePaths">
      Рассчитать
    </v-btn>
    <p>Результат:</p>
    <p>{{ multipliedMatr }}</p>
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
    multipliedMatr: null
    };
  },

  methods: {
    calculatePaths() {
      this.multipliedMatr = this.matr
      for (let i = 1; i < this.inputValue; i++) {
        console.log(i)
        this.multipliedMatr = math.multiply(this.multipliedMatr, this.matr)
      }
    }
  },
};
</script>

<style lang="scss" scoped>

</style>