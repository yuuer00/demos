<template>
  <div class="home">
    <!-- <div>{{ checkedValue }}</div> -->
    <div class="d-flex">
      <cascader-panel
        :options="options"
        :props="props"
        v-model="checkedValue"
        :setting="setting"
      ></cascader-panel>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import cascaderPanel from "@/components/cascader-panel/cascader-panel";
import { options } from "./data";
export default {
  name: "Home",
  components: { cascaderPanel },
  data() {
    return {
      checkedValue: [],
      options: options,
      props: { multiple: true },
      setting: [
        {
          title: "类型", // 标题
          multiple: false, // 此级是否支持多选(注意！true之后不能出现false)
          isshowallcheck: false // 是否显示全选按钮，为true时，multiple必须为true
        },
        { title: "组件", multiple: true, isshowallcheck: true },
        { title: "功能", multiple: true, isshowallcheck: true }
      ]
    };
  }
};
</script>
<style lang="less" scoped>
.d-flex {
  display: flex;
}
</style>
