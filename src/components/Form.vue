<template>
    <ElCard class="form-card">
      <ElForm :model="formData" ref="addItemForm" :rules="rules" lable-position="top">
          <ElFormItem label="Type" prop="type">
              <ElSelect class="type-select" v-model="formData.type" placeholder="Choose type...">
                  <ElOption label="Income" value="INCOME"/>
                  <ElOption label="Outcome" value="OUTCOME"/>
              </ElSelect>
          </ElFormItem>
          <ElFormItem label="Comments" prop="comment">
              <ElInput v-model="formData.comment"/>
          </ElFormItem>
          <ElFormItem label="Value" prop="value">
              <ElInput v-model.number="formData.value"/>
          </ElFormItem>
          <ElButton @click="onSubmit" type="primary">Submit</ElButton>
      </ElForm>
    </ElCard>
</template>

<script>
    export default {
        name: "Form",
        data: () => ({
            formData: {
                type: 'INCOME',
                comment: '',
                value: 0,
            },
            rules: {
                type: [{required: true, message: 'Please select type', trigger: 'blur'}],
                comment: [{required: true, message: 'Please input comment', trigger: 'change'}],
                value: [
                    {required: true, message: 'Please input value', trigger: 'change'},
                    {type: 'number', message: 'Value must be a number', trigger: 'change'},
                    {validator: (rule, value, callback) => {
                            if(value !== 0){
                                callback();
                            } else {
                                callback('Zero is not acceptable');
                            }
                        }, trigger: 'blur'}],
            },
        }),
        methods: {
            onSubmit() {
                this.$refs.addItemForm.validate(valid => {
                    if (valid) {
                        const valueTotalBalance = {...this.formData};
                        this.inputValueType(valueTotalBalance);
                        this.$emit('submitForm', valueTotalBalance);
                        this.$refs.addItemForm.resetFields();
                    }
                });
            },
            inputValueType(valueType) {
                if (valueType.type === 'INCOME') {
                    valueType.value = Math.abs(valueType.value);
                }
                if (valueType.type === 'OUTCOME') {
                    valueType.value = -Math.abs(valueType.value);

                }
            },
        },
    };
</script>

<style scoped>
.form-card {
    max-width: 500px;
    margin: auto;
}
.type-select {
    width: 100%;
}
</style>
