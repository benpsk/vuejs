<template>
  <div class="tic-tac-toe">
    <div class="board">
      <div class="row" v-for="(row, i) in board" :key="i">
        <Cell v-for="(cell, j) in row" 
        :key="j" 
        :row="i" 
        :player="player" 
        :col="j"
        :cell="cell"
        @click="makeMove" />
      </div>
    </div>
    <div v-if="winner">{{ winner }} wins!</div>
    <div v-else-if="isDraw">It's a draw!</div>
    <div v-else>Play</div>
  </div>
</template>

<script>
import Cell from "./components/Cell.vue";

export default {
  components: {
    Cell
  },
  data() {
    return {
      board: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],
      player: "X",
      winner: null,
      isDraw: false,
    };
  },
  methods: {
    makeMove(row, col) {
      if (!this.winner && !this.board[row][col]) {
        this.board[row][col] = this.player;
        this.checkForWinner();
        this.player = this.player === "X" ? "O" : "X";
      }
    
    },
    checkForWinner() {
      const board = this.board;
      const winningRows = [
        [board[0][0], board[0][1], board[0][2]],
        [board[1][0], board[1][1], board[1][2]],
        [board[2][0], board[2][1], board[2][2]],
        [board[0][0], board[1][0], board[2][0]],
        [board[0][1], board[1][1], board[2][1]],
        [board[0][2], board[1][2], board[2][2]],
        [board[0][0], board[1][1], board[2][2]],
        [board[2][0], board[1][1], board[0][2]],
      ];
      for (let i = 0; i < winningRows.length; i++) {
        const [a, b, c] = winningRows[i];
        if (a && a === b && b === c) {
          this.winner = a;
          this.isDraw = true;
          return;
        }
      }
    }
  }
}
</script>

<style>
.tic-tac-toe {
  font-family: "Arial", sans-serif;
  text-align: center;
  margin: 0 auto;
}

.board {
  display: inline-block;
  border-collapse: collapse;
  border: 2px solid #999;
  box-shadow: 3px 3px 5px rgba(0, 0, 0, 0.3);
}

.row {
  display: table-row;
}
</style>
