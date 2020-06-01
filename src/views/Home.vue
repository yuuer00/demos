<template>
  <div class="home">
    <div class="d-flex" style="display:none;">
      <ducascader
        :options="options"
        v-model="checkedValue"
        :setting="setting"
        :iszip="iszip"
        :props="props"
      ></ducascader>
    </div>
    <!-- {{ checkedValue }} -->
    <div style="margin: 20px auto;width:700px;">
      <selection :setting="mock" @change="handleSelectionChange"></selection>
    </div>
  </div>
</template>

<script>
const mock = [
  {
    id: 0,
    name: "微信公众号与小程序",
    description: "基于微信公众号、小程序与小游戏生态的广告场景",
    site: ["wechat"], // 数组长度大于1, 该项显示两个小选项
    type: "0" // 1--多选， 0 单选
  },
  {
    id: 1,
    name: "QQ、腾讯看点、腾讯音乐",
    description: "QQ、QQ空间、看点、浏览器、QQ音乐、全民K歌等媒体",
    site: ["qq", "andro"],
    type: "1" // 1--多选， 0 单选
  },
  {
    id: 2,
    name: "腾讯新闻与腾讯视频",
    description: "腾讯新闻、腾讯视频、腾讯体育等媒体",
    site: ["link", "ios"],
    type: "1" // 1--多选， 0 单选
  },
  {
    id: 3,
    name: "优量汇",
    description: "集合数万优质媒体海量曝光",
    site: ["app"],
    type: "1" // 1--多选， 0 单选
  },
  {
    id: 4,
    name: "PCQQ、QQ空间、腾讯音乐",
    description: "PCQQ、QQ空间、腾讯音乐等媒体",
    site: ["pcqq"],
    type: "0" // 1--多选， 0 单选
  }
];

// @ is an alias to /src
import ducascader from "@/components/cascader-panel/index";
import selection from "@/components/selection";
import { options } from "./data";
export default {
  name: "Home",
  components: { ducascader, selection },
  data() {
    return {
      mock,
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
  },
  methods: {
    handleSelectionChange(val) {
      console.log("handleSelectionChange", val);
    }
  }
};
</script>
<style lang="less" scoped>
.d-flex {
  display: flex;
}
</style>
