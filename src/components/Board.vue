<template>
    <div>
        <div class="status">当前玩家：{{currentPlayer}}</div>
        <div class="board-row" v-for="(row, index) in board" :key="index">
            <Square v-for="item in row" :key="item" :value="item" />
        </div>
    </div>
</template>

<script>
import Square from "./Square.vue"
export default {
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
            ]
        }
    },
    methods: {
    }
}
</script>

<style>
    .board-row:after {
        clear: both;
        content: "";
        display: table;
    }

    .status {
        margin-bottom: 10px;
    }   
</style>