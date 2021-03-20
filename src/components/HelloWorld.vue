
<script>
export default {
  data: () => ({
    counter: 0,
    matrix: [
      [0, 0, 0],
      [0, 0, 0],
      [0, 0, 0]
    ]
  }),
  props: {
    msg: String
  },
  methods: {
    getCoordinate(rowIndex,columnIndex) {
      this.counter = this.counter + 1
      console.log(rowIndex,columnIndex, this.counter)
      if (this.counter % 2 === 0) {
        this.matrix[rowIndex].splice(columnIndex,1,1)
      } else if (this.counter % 2 !== 0) {
        this.matrix[rowIndex].splice(columnIndex,1,2)
      }
      console.log(this.matrix)
      // console.log(this.matrix[2].slice())
      // for (let i in this.matrix) {
      //   for (let j in this.matrix[i].slice()[j]) {
      //       console.log(j)
      //     //  if (this.matrix[2].slice[j] === 2){
      //     //   console.log("circle")
      //     // } else {
      //     //   console.log('cross')
      //     // }
      //   }
      // }
    }
  },
  mounted() {
  }
}
</script>

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class="tictaktoe">
      <div v-for="(row, rowIndex) in matrix" :key="rowIndex" class="field">
        <div v-for="(column, columnIndex) in row" :key="columnIndex">
          <div
              @click="getCoordinate(rowIndex,columnIndex)"
              :class="column === 1 ? 'cross' : column === 2 ? 'circle' : 'no-clicked'"
          >
          </div>
        </div>
        <br>
      </div>
    </div>
  </div>
</template>

<style scoped>
.clicked {

}
.cross {
  background: url("../assets/cross.svg") no-repeat center;
  background-size: 30px 30px;
  pointer-events: none;
}
.circle {
  background: url("../assets/circle.svg") no-repeat center;
  background-size: 30px 30px;
  pointer-events: none;
}
.no-clicked {
}
h3 {
  margin: 40px 0 0;
}
.field div{
  width: 40px;
  border: 1px solid #404D59;
  min-height: 40px;
}
.field div:first-child {
  border-top: none;
}
.field div:nth-child(3) div,
.field div:nth-child(3) {
  border-bottom: none;
}
.field:last-child div {
  border-right: none;
  border-left: none;
}
.field:first-child div {
  border-right: none;
  border-left: none;
}

.tictaktoe {
  display: flex;
  justify-content: center;
  margin: 0 auto;
}
</style>
