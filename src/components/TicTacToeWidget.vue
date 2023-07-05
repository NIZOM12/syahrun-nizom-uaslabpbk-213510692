<template>
  <div id="app">
    <h1>Tic Tac Toe</h1>
    <div class="board">
      <div v-for="(cell, index) in board" :key="index" class="cell" @click="makeMove(index)">
        {{ cell }}
      </div>
    </div>
    <div v-if="winner !== null" class="message">{{ winner }}</div>
    <button @click="resetGame">Mulai Ulang</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      board: Array(9).fill(null),
      currentPlayer: "X",
      winner: null,
    };
  },
  methods: {
    makeMove(index) {
      if (this.board[index] === null && this.winner === null) {
        this.board.splice(index, 1, this.currentPlayer);
        if (this.checkWin()) {
          this.winner = this.currentPlayer + " menang!";
        } else if (!this.board.includes(null)) {
          this.winner = "Seri";
        } else {
          this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
        }
      }
    },
    checkWin() {
      const winCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      for (let combination of winCombinations) {
        const [a, b, c] = combination;
        if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
          return true;
        }
      }

      return false;
    },
    resetGame() {
      this.board = Array(9).fill(null);
      this.currentPlayer = "X";
      this.winner = null;
    },
  },
};
</script>

<style>
#app {
  text-align: center;
}

h1 {
  font-size: 24px;
  margin-bottom: 20px;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  max-width: 300px;
  margin: 0 auto;
  padding: 10px;
  border: 1px solid black;
}

.cell {
  width: 100px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 24px;
  border: 1px solid black;
  cursor: pointer;
}

.message {
  margin-top: 20px;
  font-size: 18px;
  color: #2196f3;
}

button {
  margin-top: 10px;
  padding: 10px 20px;
  font-size: 16px;
  background-color: #2196f3;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #1976d2;
}

button:active {
  background-color: #1565c0;
}
</style>
