<template>
  <div id="app">
    <DeleteItemDialog :dialogHidden="dialogHidden" @closeDialog="showDialog" @deleteItem="deleteIt"/>
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList :fList="filterList" @deleteItem="onDeleteItem" @onListShow="onListShow"/>
  </div>
</template>

<script>
import BudgetList from "./components/BudgetList";
import TotalBalance from "./components/TotalBalance";
import Form from "./components/Form";
import DeleteItemDialog from "./helpers/DeleteItemDialog";

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form,
    DeleteItemDialog
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comments',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comments',
        id: 2,
      },
    },
    dialogHidden: { type: false, list: Number},
    fList: null
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => acc + item.value, 0)
    },
    filterList() {
      if(!this.fList){
        return this.list
      }
      return this.fList;
    }
  },
  methods: {
    onDeleteItem(id) {
      this.showDialog();
      this.dialogHidden.list = this.list[id];
    },
    onListShow(param){
      if(param === 1) {
        this.fList  = Object.values(this.list).filter(item => item.value > 0).reduce((acc, val) => {acc[val.id] = val; return acc},{})
      }else if (param === -1){
        this.fList  = Object.values(this.list).filter(item => item.value < 0).reduce((acc, val) => {acc[val.id] = val; return acc},{})
      }else {
        this.fList  = this.list;
      }
    },
    onFormSubmit(data){
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj);
    },
    showDialog() {
      this.dialogHidden.type = !this.dialogHidden.type;
    },
    deleteIt(id) {
      this.$delete(this.list, id.id);
      this.showDialog();
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
