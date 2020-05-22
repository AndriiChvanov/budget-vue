<template>
         <el-dialog title="Budget list" :visible.sync="dialogHidden.type"
                    width="30%"
                    :before-close="dialogClose"
                    append-to-body>
            <span class="negative">Do you really want to delete ?</span>
            <div>{{dialogHidden.list.type}}: {{dialogHidden.list.comment}}   {{dialogHidden.list.value}}$</div>
            <span  slot="footer" class="dialog-footer">
                <el-button  type="danger" @click="dialogClose">Cancel</el-button>
                <el-button type="success" @click="confirmClose">Confirm</el-button>
            </span>
        </el-dialog>
</template>

<script>
    export default {
        props: ['dialogHidden'],
        data() {
            return {};
        },
        methods: {
            dialogClose() {
              this.$emit('closeDialog')
            },
            confirmClose(){
                this.$emit('deleteItem', this.dialogHidden.list)
            }
        }
    }
</script>

<style scoped>
    .negative{
        color: #F56C6C;
    }
</style>
