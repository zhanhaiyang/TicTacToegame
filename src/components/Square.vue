<template>
    <button class="square" @click="setValue">
        {{ value }}
    </button>
</template>

<script>
export default {
    props: ['value'],
    data() {
        return {}
    },
    methods: {
        setValue() {
            this.$emit('click')
        }
    }
}
</script>

<style>
    .square {
        background: #fff;
        border: 1px solid #999;
        float: left;
        font-size: 24px;
        font-weight: bold;
        line-height: 34px;
        height: 34px;
        margin-right: -1px;
        margin-top: -1px;
        padding: 0;
        text-align: center;
        width: 34px;
    }

    .square:focus {
        outline: none;
    }
</style>