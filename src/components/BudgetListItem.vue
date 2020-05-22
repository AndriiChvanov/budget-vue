<template>
<div>
    <div class="list-item">
        <div class="budget-comment" :style="{color: setColor}">{{ item.comment }}</div>
        <div class="budget-value" :style="{color: setColor}">{{ item.value }}
            <i class="el-icon-top" v-if="item.type === 'INCOME'"></i>
            <i class="el-icon-bottom" v-else></i>
        </div>
        <ElButton type="danger" size="mini" @click="deleteItem(item.id)" >Delete</ElButton>
    </div>
</div>
</template>

<script>
    export default {
        name: "BudgetListItem",
        props: {
            item: {
                type: Object,
                default: () => ({})
            },
        },
        computed:{
          setColor() {
              return this.item.type === 'INCOME' ? 'green' : 'red'
          }
        },
        methods: {
            deleteItem(id) {
                this.$emit('deleteItem', id);
            },
        },
    }
</script>

<style scoped>
    .list-item {
        display: flex;
        align-items: center;
        padding: 10px 15px;
    }
    .budget-value {
        font-weight: bold;
        margin-left: auto;
        margin-right: 20px;
    }
</style>
