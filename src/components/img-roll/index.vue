<template>
  <div class="img_roll" :style="{ height: height + 'px' }">
    <img
      class="img_roll_img"
      :src="url"
      @load="handleImgLoad"
      alt="img"
      ref="img_roll_img"
      :style="{ bottom }"
    />
  </div>
</template>

<script>
export default {
  props: ["height", "url"],
  data() {
    return {
      bottom: "auto"
    };
  },
  methods: {
    handleImgLoad() {
      if (this.height >= this.$refs.img_roll_img.height) {
        this.bottom = "auto !important";
        return;
      }
      this.bottom = this.height - this.$refs.img_roll_img.height + "px";
    }
  }
};
</script>

<style lang="less" scoped>
.img_roll {
  width: 200px;
  overflow: hidden;
  font-size: 0;
  position: relative;
  .img_roll_img {
    position: absolute;
    width: 100%;
    transition: bottom 0.6s;
  }
  &:hover {
    .img_roll_img {
      bottom: 0 !important;
    }
  }
}
</style>