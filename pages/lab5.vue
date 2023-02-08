<template>
  <div>
    <h1>Задание 1</h1>
    <p>10. Скорость первого автомобиля V1 км/ч, второго — V2 км/ч,
расстояние между ними S км. Определить расстояние между ними
через T часов, если автомобили первоначально движутся навстречу
друг другу. </p>
    <v-row>
      <v-col
      cols="3">
        <v-text-field
        v-model="v1"
        placeholder="Скорость V1">
        </v-text-field>
      </v-col>
      <v-col
      cols="3">
        <v-text-field
        v-model="v2"
        placeholder="Скорость V2">
        </v-text-field>
      </v-col>
      <v-col
      cols="3">
        <v-text-field
        placeholder="Расстояние S"
        v-model="s">
        </v-text-field>
      </v-col>
      <v-col
      cols="3">
        <v-text-field
        v-model="t"
        placeholder="Время T">
        </v-text-field>
      </v-col>
      <v-btn
      @click="calculateS">
        Посчитать
      </v-btn>
      <p>
        {{ sResult }}
      </p>
    </v-row>
    <h1>Задание 2</h1>
    <p>10. Дан номер некоторого года (целое положительное число).
Определить соответствующий ему номер столетия, учитывая, что, к
примеру, началом 20 столетия был 1901 год. </p>
      <v-text-field
      v-model="year"
      placeholder="Введите год">1998
      </v-text-field> 
      <v-btn
      @click="calculateCentury">
        Посчитать
      </v-btn>
      <p>
        Столетие: {{ century }}
      </p>
    <h1>Задание 3</h1>
    <p>10. Даны координаты поля шахматной доски x, y (целые числа,
лежащие в диапазоне 1-8). Учитывая, что левое нижнее поле доски
(1, 1) является черным, проверить истинность высказывания:
«Данное поле является белым». </p>
      <v-row>
        <v-col
        cols="6">
          <v-text-field
          v-model="x"
          placeholder="Введите значение x">

          </v-text-field>
        </v-col>
        <v-col
        cols="6">
          <v-text-field
            v-model="y"
            placeholder="Введите значение y">

          </v-text-field>
        </v-col>
        <v-btn
        @click="isBlack">
          Посчитать
        </v-btn>
        <p>
          {{ black }}
        </p>
      </v-row>
  </div>
</template>

<script>
export default {
  name: 'ParcalcLab5',

  data() {
    return {
      v1: null,
      v2: null,
      s: null,
      t: null,
      sResult: null,
      year: null,
      century: null,
      x: null,
      y: null,
      black: false,
    };
  },

  mounted() {
    
  },

  methods: {
    calculateS() {
      this.sResult = Number(this.s) - ((Number(this.v1)  + Number(this.v2)) * Number(this.t))
    },
    calculateCentury() {
      const year = Number(this.year)
      if (year % 100 === 0) {
        this.century = year / 100
      } else {
        this.century = Math.floor(year/100+1)
      }
    },
    isBlack() {
      if (this.x > 8 || this.y < 1 || this.x < 1 || this.y > 8) {
        this.black = 'Координаты должны быть в диапазоне от 1 до 8'
        return
      }
      this.black = Boolean((this.x % 2 === 0) ^ (this.y % 2 === 0))
    }
  },
};
</script>

<style lang="scss" scoped>

</style>