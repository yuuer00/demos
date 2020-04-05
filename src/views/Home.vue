<template>
  <div class="home">
    <div class="d-flex">
      <cascader-panel :options="options"></cascader-panel>
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
      options: options
    };
  }
};
</script>
<style lang="less" scoped>
.d-flex {
  display: flex;
}
</style>
