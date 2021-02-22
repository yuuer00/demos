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
    <div style="margin: 20px auto;width:700px;display:none;">
      <selection
        :setting="mock"
        @change="handleSelectionChange"
        v-model="checkSite"
      ></selection>
    </div>
    <!-- <el-button @click="checkSite = ['qq', 'app', 'ios']">设置多选</el-button>
    <el-button @click="checkSite = ['pcqq']">设置单选</el-button>
    <h3>切记！！！如果pcqq是单选，设置的时候，不能设置['pcqq','qq']这样</h3> -->

    <img-roll
      :height="200"
      url="https://qcloudtest-1255506820.cos.ap-guangzhou.myqcloud.com/images/col1.jpg"
    ></img-roll>
    <div>
      <div>{{ dayvalue }}</div>
      <dayInput v-model="dayvalue"></dayInput>
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
    type: "0", // 1--多选， 0 单选
  },
  {
    id: 1,
    name: "QQ、腾讯看点、腾讯音乐",
    description: "QQ、QQ空间、看点、浏览器、QQ音乐、全民K歌等媒体",
    site: ["qq", "andro"],
    type: "1", // 1--多选， 0 单选
  },
  {
    id: 2,
    name: "腾讯新闻与腾讯视频",
    description: "腾讯新闻、腾讯视频、腾讯体育等媒体",
    site: ["link", "ios"],
    type: "1", // 1--多选， 0 单选
  },
  {
    id: 3,
    name: "优量汇",
    description: "集合数万优质媒体海量曝光",
    site: ["app"],
    type: "1", // 1--多选， 0 单选
  },
  {
    id: 4,
    name: "PCQQ、QQ空间、腾讯音乐",
    description: "PCQQ、QQ空间、腾讯音乐等媒体",
    site: ["pcqq"],
    type: "0", // 1--多选， 0 单选
  },
];

// @ is an alias to /src
import ducascader from "@/components/cascader-panel/index";
import selection from "@/components/selection";
import imgRoll from "@/components/img-roll";
import dayInput from "@/components/dayInput";
import { options } from "./data";
export default {
  name: "Home",
  components: { ducascader, selection, imgRoll, dayInput },
  data() {
    return {
      mock,
      checkSite: [],
      checkedValue: [],
      options: options,
      props: { multiple: true, value: "id", label: "name", children: "child" },
      iszip: true,
      dayvalue: [],
      setting: [
        {
          title: "类型", // 标题
          multiple: true,
          isshowallcheck: true, // 是否显示全选按钮，为true时，multiple必须为true
        },
        { title: "测试", multiple: true, isshowallcheck: true },
        { title: "", multiple: true, isshowallcheck: true },
        { title: "", multiple: true, isshowallcheck: true },
      ],
    };
  },
  methods: {
    handleSelectionChange(val) {
      console.log("handleSelectionChange", val);
      console.log("this.checkSite", this.checkSite);
    },
  },
};
</script>
<style lang="less" scoped>
.d-flex {
  display: flex;
}
</style>
