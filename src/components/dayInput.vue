<template>
  <div class="input-box">
    <template v-for="(item, index) in dataLen">
      <div :key="item" class="input-item">
        <div class="day-t">{{ dataWords[index] }}</div>
        <div class="day-b">
          <el-input v-model="data[index]"></el-input>
        </div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Array,
      default: () => {
        return [];
      },
    },
    dataLen: {
      type: Number,
      default: 7,
    },
  },
  data() {
    return {
      dataWords: ["一", "二", "三", "四", "五", "六", "日"],
    };
  },
  computed: {
    data: {
      get() {
        return this.value;
      },
    },
  },
};
</script>

<style lang="less" scoped>
.input-box {
  display: flex;
}
</style>
