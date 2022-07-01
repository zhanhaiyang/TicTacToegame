<template>
  <div>
    <div class="game">
      <div class="game-board">
        <Board :squares="history[this.stepNumber].squares" @click="handleClick" />
      </div>
      <div class="game-info">
        <div>{{ isStop ? '对局结束，获胜者为：' + currentPlayer : '当前玩家：' + currentPlayer }}</div>
        <ol>
          <li v-for="(squares, index) in history" :key="index" :class="{ 'move-on': index === stepNumber }">
            <button @click="jumpTo(index)">{{ 0 === index ? '回到开始' : '回到步骤#' + index }}</button>
          </li>
        </ol>

      </div>
    </div>
  </div>
</template>

<script>
import Board from './Board.vue'
export default {
  components: {
    Board
  },
  data() {
    return {
      history: [{
        squares: Array(9).fill(null),
      }],
      xIsNext: true,
      isStop: false,
      currentPlayer: `X`,
      stepNumber: 0,
      winner: {
        step: 0,
        player: ''
      }
    }
  },
  methods: {
    handleClick(i) {
      const history = this.history.slice(0, this.stepNumber + 1);;
      const current = history[history.length - 1]
      const squares = current.squares.slice();
      const result = this.win(squares);
      if (result) {
        alert('胜负已定！');
        return;
      }
      if (squares[i]) {
        alert('该位置已被占!');
        return
      };
      squares[i] = this.xIsNext ? 'X' : 'O';
      this.history = history.concat([{
        squares: squares
      }]);
      this.stepNumber = history.length;
      if (this.win(squares)) {
        alert('胜负已定！获胜的是:' + this.currentPlayer);
        this.isStop = true;
        this.winner = { step: history.length, player: this.currentPlayer }
        return;
      }
      this.xIsNext = !this.xIsNext;
      this.currentPlayer = this.xIsNext ? 'X' : 'O'
      if(this.stepNumber===9){
        alert('平局')
      }
    },
    win(squares) {
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
        const [a, b, c] = lines[i]; // a, b, c 为棋盘下标
        //squares[a] 为棋子
        if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
          return squares[a];
        }
      }
      return null;
    },
    jumpTo(step) {
      if (step === this.stepNumber) {
        alert('已在' + (0 === step ? '最开始' : `步骤#${step}！`));
        return;
      }
      if (step === this.winner.step) {
        this.isStop = true
      } else {
        this.isStop = false
      }
      this.stepNumber = step;
      this.xIsNext = (step % 2) === 0;
      this.currentPlayer = this.xIsNext ? 'X' : 'O'
    }
  }
}
</script>

<style>
.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}

.game-info button {
  outline: none;
  border-radius: 5px;
}

.game-info button:hover {
  border-color: #666;
}

.move-on button {
  border-color: #000;
}
</style>