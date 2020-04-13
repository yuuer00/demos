<template>
  <div class="home">
    <div>{{ checkedValue }}11</div>
    <div class="d-flex">
      <cascader-panel
        :options="options"
        :zip="true"
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
      // checkedValue: [
      //   ["zhinan", "shejiyuanze", "fankui"],
      //   ["zhinan", "shejiyuanze", "xiaolv"]
      // ],
      checkedValue: ["zhinan"],
      options: options,
      props: { multiple: true },
      setting: [
        {
          title: "类型", // 标题
          multiple: true,
          isshowallcheck: true // 是否显示全选按钮，为true时，multiple必须为true
        },
        { title: "测试", multiple: true, isshowallcheck: true },
        { title: "", multiple: true, isshowallcheck: true }
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
