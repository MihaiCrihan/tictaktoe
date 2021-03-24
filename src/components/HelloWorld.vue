
<script>
export default {
  data: () => ({
    counter: 0,
    matrix: [
      [0, 0, 0],
      [0, 0, 0],
      [0, 0, 0]
    ],
    winCombination: [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
    ],
    gameState: ["", "", "", "", "", "", "", "", ""]
  }),
  props: {
    msg: String
  },
  methods: {
    getCoordinate(rowIndex,columnIndex) {
      this.counter = this.counter + 1
      // console.log(rowIndex,columnIndex, this.counter)
      if (this.counter % 2 === 0) {
        this.matrix[rowIndex].splice(columnIndex,1,1)
      } else if (this.counter % 2 !== 0) {
        this.matrix[rowIndex].splice(columnIndex,1,2)
      }
        // this.matrix.forEach((item, index) => {
        //   if (
        //       this.counter > 3 &&
        //       ([...new Set(item)].length <= 1 ||
        //       [...new Set([this.matrix[0][index], this.matrix[1][index], this.matrix[2][index]])].length <= 1)
        //   ) {
        //     console.log("win!");
        //   }
        // });
      this.winCombination.forEach((item, index) => {
        const winCondition = item[index];
        const a = this.gameState[winCondition[0]];
        const b = this.gameState[winCondition[1]];
        const c = this.gameState[winCondition[2]];
        console.log(this.gameState[winCondition[0]]);
        if (a === '' || b === '' || c === '') {
          console.log("ce")
        }
        if (a === b && b === c) {
          console.log("a cistigat")
        }
      })
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
  /*transform: rotate(90deg);*/
  justify-content: center;
  margin: 0 auto;
}
</style>
