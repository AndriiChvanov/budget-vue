<template>
    <div class="total-value">
        <template v-if="total > 0">
        <span class="positive">Balance: {{ total }}</span>
    </template>
        <template v-else-if="total < 0">
            <span class="negative">Balance: {{ total }}</span>
        </template>
        <template v-else>
            <span class="zero">Balance: {{ total }}</span>
        </template></div>
</template>

<script>
    export default {
        name: "TotalBalance",
        props: {
            total: {
                type: Number,
                default: 0
            },
        },
    };
</script>

<style scoped>
.total-value {
    font-size: 26px;
    text-transform: uppercase;
    padding: 20px;
    text-align: center;
}
.positive{
    color: #67C23A;
}
.negative{
    color: #F56C6C;
}
.zero{
    color: #000;
}
</style>
