<template>
    <div class="cell" @click="onClick">
        {{ cell }}
    </div>
</template>

<script lang="ts">
export default {
    props: {
        cell: {
            type: String,
            default: "",
        },
        row: {
            type: Number,
            required: true,
        },
        col: {
            type: Number,
            required: true,
        },
        player: {
            type: String,
            required: true
        }
    },
    methods: {
        onClick() {
            if (!this.cell) {
                this.$emit("click", this.row, this.col);
            }
        }
    }
}
</script>


<style scoped>
.cell {
    display: table-cell;
    width: 50px;
    height: 50px;
    font-size: 36px;
    font-weight: bold;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    user-select: none;
    border: 1px solid #999;
}
</style>
