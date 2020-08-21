<template>
  <div>
    <el-checkbox-group
      :value="checkList"
      @input="handleCheckboxChange"
      ref="ECG"
    >
      <el-checkbox-button :label="3">复选框 A</el-checkbox-button>
      <el-checkbox-button :label="6">复选框 B</el-checkbox-button>
      <el-checkbox-button :label="9">复选框 C</el-checkbox-button>
    </el-checkbox-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      checkList: []
    };
  },
  methods: {
    handleCheckboxChange(val) {
      this.$refs.ECG.$children.forEach(label => {
        // 注意此处checkboxNode.value的类型
        // 当为el-checkbox-button时，只需将下面换成.el-checkbox-button__original
        let checkboxNode = label.$el.querySelector(
          ".el-checkbox-button__original"
        );
        // let checkboxNode = label.$el.querySelector(".el-checkbox__original");
        checkboxNode &&
          (checkboxNode.checked = !!this.checkList.filter(
            item => item == checkboxNode.value
          ).length);
      });
      this.$confirm("是否修改？", "提示", {
        type: "warning"
      })
        .then(() => {
          this.checkList = val;
        })
        .catch(error => {
          console.log(error);
          // site字段在当前数组是唯一的
          let arr = [
            {
              name: "name",
              description: "描述",
              site: ["link", "ios"], // 数组长度大于1, 该项显示两个小选项
              type: "1" // 1--多选， 0 单选
            },
             {
              name: "name",
              description: "描述",
              site: ["qq", "andro"],
              type: "1" // 1--多选， 0 单选
            },
            {
              name: "name",
              description: "描述",
              site: ["app"],
              type: "1" // 1--多选， 0 单选
            },
            {
              name: "name",
              description: "描述",
              site: ["pcqq"],
              type: "0" // 1--多选， 0 单选
            },
            {
              name: "name",
              description: "描述",
              site: ["wechat"],
              type: "0" // 1--多选， 0 单选
            }
          ];
        });
    }
  }
};
</script>
