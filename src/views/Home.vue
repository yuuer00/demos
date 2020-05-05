<template>
  <div class="home">
    <div class="d-flex">
      <ducascader
        :options="options"
        v-model="checkedValue"
        :setting="setting"
        :iszip="iszip"
        :props="props"
      ></ducascader>
    </div>
    {{ checkedValue }}
  </div>
</template>

<script>
// @ is an alias to /src
import ducascader from "@/components/cascader-panel/index";
import { options } from "./data";
export default {
  name: "Home",
  components: { ducascader },
  data() {
    return {
      checkedValue: [],
      options: options,
      props: { multiple: true, value: "id", label: "name", children: "child" },
      iszip: true,
      setting: [
        {
          title: "类型", // 标题
          multiple: true,
          isshowallcheck: true // 是否显示全选按钮，为true时，multiple必须为true
        },
        { title: "测试", multiple: true, isshowallcheck: true },
        { title: "", multiple: true, isshowallcheck: true },
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
