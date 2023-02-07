<template>
  <div>
    <h1>
      Стек:
    </h1>
    <v-text-field
    v-model="stackInput"
    placeholder="Введите элемент стека">
    </v-text-field>
    <v-btn
    @click="addToStack">
      Добавить элемент в стек
    </v-btn>
    <p>
      Результат работы программы: {{ stackReturn }}
    </p>
    <h1>
      Очередь:
    </h1>
    <v-text-field
    v-model="queueInput"
    placeholder="Введите элемент очереди">
    </v-text-field>
    <v-btn
    @click="addToQueue">
      Добавить элемент в очередь
    </v-btn>
    <p>
      Результат работы программы: {{ queueReturn }}
    </p>
    <h1>
      Список:
    </h1>
    <v-text-field
    v-model="listInput"
    placeholder="Введите элемент списка">
    </v-text-field>
    <v-btn
    @click="addToList">
      Добавить элемент в список
    </v-btn>
    <p>
      Результат работы программы: {{ listReturn }}
    </p>
    <v-text-field
    v-model="keyInput"
    placeholder="Введите ключ">
    </v-text-field>
    <v-row>
      <v-col
      cols="6">
        <v-btn
        @click="deleteElementFromList">
          Удалить элемент
        </v-btn>
      </v-col>
      <v-col
      cols="6">
      <v-text-field
      v-model="addListElementInput"
      placeholder="Введите элемент">
      </v-text-field>
      <v-btn
      @click="addElementToList">
        Вставить элемент
      </v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: 'ParcalcLab4',

  data() {
    return {
      stackInput: null,
      stack: [],
      stackReturn: [],
      queueInput: null,
      queue: [],
      queueReturn: [],
      listInput: null,
      list: [],
      listReturn: [],
      keyInput: null,
      addListElementInput: null,
      showListControl: false
    };
  },

  mounted() {

  },

  methods: {
    addToStack () {
      if (this.stackInput !== 'END') {
        this.stack.unshift(this.stackInput)
      } else {
        this.stackReturn = this.stack
        this.stack = []
      }
    },
    addToQueue () {
      if (this.queueInput !== 'END') {
        this.queue.push(this.queueInput)
      } else {
        this.queueReturn = this.queue
        this.queue = []
      }
    },
    addToList () {
      if (this.listInput !== 'END') {
        this.list.push({value: this.listInput, key: this.list.length})
        this.showListControl = true
      } else {
        this.listReturn = this.list
      }
    },
    deleteElementFromList() {
      this.list.forEach((element, index, arr) => {
        if (element.key === Number(this.keyInput)) {
          arr.splice(index, 1)
        }
      })
    },
    addElementToList() {
      let flag = false
      let ind
      this.list.forEach((element, index) => {
        if (element.key === Number(this.keyInput)) {
          ind = index + 1
          flag = true
        }
      })
      if (flag === true) {
        this.list.splice(ind, 0, {value: this.addListElementInput, key: this.list.length + 1})
      }
    }
  },
};
</script>

<style lang="scss" scoped>

</style>