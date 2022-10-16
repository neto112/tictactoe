<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="game">
    <div class="game-board">
      <Board :squares="history[this.stepNumber].squares" @click="handleClick" />
    </div>
    <div class="game-info">
      <div>{{ status }}</div>
      <ol>
        <li
          v-for="(squares, index) in history"
          :key="index"
          :class="{ 'move-on': index === stepNumber }"
        >
          <button @click="jumpTo(index)">
            {{ 0 === index ? "Go to start" : "Go to move#" + index }}
          </button>
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import Board from "./Board.vue";

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
export default {
  components: {
    Board,
  },
  data() {
    return {
      history: [{ squares: Array(9).fill(null) }],
      stepNumber: 0,
      xIsNext: true,
      status: `${this.nextLabel}X`,
    };
  },
  methods: {
    handleClick(i) {
      const history = this.history.slice(0, this.stepNumber + 1);
      const current = history[history.length - 1];
      const squares = current.squares.slice();
      if (calculateWinner(squares)) {
        alert("Winner was determined!");
        return;
      }
      if (squares[i]) {
        alert("Place was taken!");
        return;
      }
      squares[i] = this.xIsNext ? "X" : "O";
      this.history = history.concat([
        {
          squares: squares,
        },
      ]);
      this.stepNumber = history.length;
      this.squares = squares;
      const winner = calculateWinner(squares);
      if (winner) {
        this.status = "Winner: " + winner;
        return;
      }
      this.xIsNext = !this.xIsNext;
      this.status = `${this.nextLabel}${this.xIsNext ? "X" : "O"}`;
    },
    jumpTo(step) {
      if (step === this.stepNumber) {
        alert("Already at " + (0 === step ? "Beginning" : `Step#${step}!`));
        return;
      }
      this.stepNumber = step;
      this.xIsNext = step % 2 === 0;
      // eslint-disable-next-line no-undef
      this.status = `${this.nextLabel}${this.xIsNext ? "X" : "O"}`;
    },
  },
};
</script>

