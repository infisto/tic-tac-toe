<template>
  <div class="content">
    <div class="result">
      <h2>{{ winner }}</h2>
      <h2 v-if="end">Игра окончена</h2>
    </div>
    <div class="wrapper" ref="board">
      <div v-for="(elem, index) in 9" :key="index" class="cell"
           @click="(!loading && !end) ? handleClick(index, $event) : null"
      >
      </div>
    </div>
    <button @click="refresh">Обновить</button>
  </div>

</template>

<script>
export default {
  name: "TicTacToe",
  data() {
    return {
      sequence: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ],
      winner: "",
      loading: false,
      end: false
    };
  },
  methods: {
    handleClick(index, event) {
      if (event.target.textContent === "X" || event.target.textContent === "O") return;
      event.target.textContent = "X";
      if (this.check(this.sequence) === "player") {
        this.winner = "Вы победили";
        this.end = true;
        return;
      }
      this.loading = true;
      this.computerRun();
    },
    computerRun() {
      new Promise(resolve => {
        setTimeout(() => {
          resolve();
        }, 1000);
      }).then(() => {
        this.loading = false;
        const cells = [...this.$refs.board.childNodes].map(elem => {
          if (elem.textContent !== "X" && elem.textContent !== "O") {
            return elem;
          }
        }).filter(elem => elem);
        if (cells.length > 0) {
          let randomCell = this.arrayRandElement(cells);
          randomCell.textContent = "O";
          if (this.check(this.sequence) === "computer") {
            this.winner = "Победил ПК";
            this.end = true;
            return;
          }
        }
      });
    },
    arrayRandElement(arr) {
      return arr[Math.floor(Math.random() * arr.length)];
    },
    check(arr) {
      const cells = [...this.$refs.board.childNodes];
      for (let i = 0; i < arr.length; i++) {
        if (cells[arr[i][0]].textContent === "X" && cells[arr[i][1]].textContent === "X" && cells[arr[i][2]].textContent === "X") {
          return "player";
        } else if (cells[arr[i][0]].textContent === "O" && cells[arr[i][1]].textContent === "O" && cells[arr[i][2]].textContent === "O") {
          return "computer";
        } else if (cells.filter(item => item.textContent).length === 9) {
          this.end = true;
        }
      }
    },
    refresh() {
      [...this.$refs.board.childNodes].forEach(item => item.textContent = '');
      this.winner = "";
      this.end = false;
    }
  }
};
</script>

<style scoped>
.content {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.wrapper {
  display: flex;
  flex-wrap: wrap;
  width: 600px;
  margin: 50px auto;
  justify-content: center;
}

.cell {
  flex: 0 0 198px;
  height: 198px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 100px;
  cursor: pointer;
}

.cell:hover {
  background: #09e3cd;
  opacity: 0.5;
}

.cell:nth-child(2), .cell:nth-child(5), .cell:nth-child(8) {
  border-left: 3px solid black;
  border-right: 3px solid black;
}

.cell:nth-child(1), .cell:nth-child(2), .cell:nth-child(3), .cell:nth-child(4), .cell:nth-child(5), .cell:nth-child(6) {
  border-bottom: 3px solid black;
}

.result {
  position: absolute;
  top: 10%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

button {
  outline: none;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  background: tomato;
  width: 200px;
  border-radius: 10px;
}
button:hover {
  background: #f38470;
}
h2 {
  font-size: 36px;
}
</style>