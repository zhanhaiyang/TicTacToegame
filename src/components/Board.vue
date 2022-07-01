<template>
    <div>
        <!-- <div class="title">{{isStop?'对局结束，获胜者为：'+currentPlayer:'当前玩家：'+currentPlayer}}</div> -->
        <div class="board-row" v-for="(row, index) in board" :key="index">
            <Square v-for="item in row" :key="item" :value="squares[item]" @click="handleClick(item)" />
        </div>
    </div>
</template>

<script>
import Square from "./Square.vue"
export default {
    props: ['squares'],
    components: {
        Square
    },
    data() {
        return {
            currentPlayer: 'X',
            board: [
                [0, 1, 2],
                [3, 4, 5],
                [6, 7, 8]
            ],
            // squares: Array(9).fill(null),
            // xIsNext: true,
            // isStop:false
        }
    },
    methods: {
        handleClick(i) {
            this.$emit('click', i)
        },
        // win(squares) {
        //     //列举出赢的组合
        //     const lines = [
        //         [0, 1, 2],
        //         [3, 4, 5],
        //         [6, 7, 8],
        //         [0, 3, 6],
        //         [1, 4, 7],
        //         [2, 5, 8],
        //         [0, 4, 8],
        //         [2, 4, 6],
        //     ];
        //     for (let i = 0; i < lines.length; i++) {
        //         const [a, b, c] = lines[i];
        //         if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
        //             return squares[a];
        //         }
        //     }
        //     return null;
        // }
    }
}
</script>

<style>
.board-row:after {
    clear: both;
    content: "";
    display: table;
}

.title {
    margin-bottom: 10px;
}
</style>