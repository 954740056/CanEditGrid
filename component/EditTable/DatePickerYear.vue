<!--可编辑表格input输入框组件-->
<template>
  <div>
    <el-date-picker
      size="mini"
      style="width:100%"
      v-model="timeData"
      type="year"
      format="yyyy"
      value-format="yyyy-MM-dd"
      :disabled="field && field.disabled ? field.disabled : false"
    >
    </el-date-picker>
  </div>
</template>

<script>
export default {
  name: "datePickerYear",
  props: {
    valueDefault: String,
    editRow: Number,
    editCol: Number,
    field: Object,
    rowData: Object,
    propRuls: String
  },
  data() {
    return {
      timeData: this.valueDefault
    };
  },
  watch: {
    timeData(val) {
      this.$parent.$parent.data[this.editRow][this.$parent.$parent.headers[this.editCol].name] = val;
      let data = val;
      data = this.$parent.$parent.dateTimeChang(data);
      this.$parent.$parent.tableValidate(this.propRuls, data, this.editCol, this.editRow, 0);
      this.$emit("data-change", val, this.editRow, this.editCol, this.rowData, this.field, this.propRuls);
    },
    valueDefault: {
      deep: true,
      immediate: true,
      handler(val) {
        this.timeData = val;
      }
    }
  }
};
</script>

<style scoped></style>
