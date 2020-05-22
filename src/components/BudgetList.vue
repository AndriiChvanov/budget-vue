<template>
    <div class="budget-list-wrap">
        <ElCard :header="header">
                <el-button type="success" size="mini" plain @click="onListShow(1)">INCOME</el-button>
                <el-button type="danger" size="mini" plain @click="onListShow(-1)">OUTCOME</el-button>
                <el-button type="info" size="mini"  plain @click="onListShow()">ALL COME</el-button>
            <template v-if="!isEmpty">
                <BudgetListItem v-for="(item, prop) in fList" :key="prop" :item="item" @deleteItem="deleteItem"/>
            </template>
            <ElAlert v-else type="info" :title="emptyTitle" :closable="false"  ></ElAlert>
        </ElCard>
    </div>
</template>

<script>
    import BudgetListItem from "./BudgetListItem";
    export default {
        components: {
            BudgetListItem,
        },
        name: "BudgetList",
        props: {
            fList: {
                type: Object,
                default: () => ({})
            },
        },
        data: () => ({
            header: 'Budget List',
            emptyTitle: 'Empty List',
        }),
        computed: {
            isEmpty() {
                return !Object.keys(this.fList).length;
            },
        },
        methods: {
            deleteItem(id) {
                this.$emit('deleteItem', id);
            },
            onListShow(param){
              this.$emit('onListShow', param)
            },
        },
    };
</script>

<style scoped>
.budget-list-wrap {
    max-width: 500px;
    margin: auto;
}

</style>
