<template>
  <div class="selection">
    <div class="selection_list">
      <div
        v-for="item in setting"
        :key="item.id"
        class="selection_item"
        :class="{ active: isCheck(item.site) }"
        @click="handleItemClick(item)"
      >
        <div class="selection_checkbox" @click.stop>
          <el-checkbox
            :value="isCheck(item.site)"
            @input="handleItemClick(item)"
          ></el-checkbox>
        </div>

        <div class="selection_content">
          <div class="selection_title">{{ item.name }}</div>
          <div class="selection_des">
            {{ item.description }}
          </div>
        </div>
        <div class="selection_child" v-if="item.site.length > 1" @click.stop>
          <el-checkbox
            v-for="child in item.site"
            :key="child"
            :value="isCheck(child)"
            @input="handleChildChange(arguments[0], child)"
            >{{ child }}
          </el-checkbox>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["setting", "value"],
  data() {
    return {};
  },
  computed: {
    // 目前选中的是否单选
    isRadio() {
      let flag = false;
      for (const item of this.setting) {
        if (item.type === "0" && this.isCheck(item.site)) {
          flag = true;
          break;
        }
      }
      return flag;
    },
    checkSite: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit("input", val);
        this.$emit("change", val);
      }
    }
  },
  methods: {
    // 传入字符串（'pcqq'）或数据（['pcqq','app']）
    // 如果checkSite有任意一项，返回true，否则返回false
    isCheck(site) {
      if (typeof site === "string") {
        return this.checkSite.indexOf(site) > -1;
      }
      return site.filter(item => this.checkSite.indexOf(item) > -1).length > 0;
    },
    handleItemClick(item) {
      if (item.type === "0") {
        if (this.isCheck(item.site)) {
          this.checkSite = [];
        } else {
          this.checkSite = [].concat(item.site);
        }
      }
      if (item.type === "1") {
        if (this.isCheck(item.site)) {
          this.checkSite = this.checkSite.filter(
            site => item.site.indexOf(site) < 0
          );
        } else {
          if (this.isRadio) {
            this.checkSite = [].concat(item.site);
          } else {
            this.checkSite = this.checkSite.concat(item.site);
          }
        }
      }
    },
    handleChildChange(check, site) {
      if (check) {
        this.checkSite = this.checkSite.concat(site);
      } else {
        this.checkSite = this.checkSite.filter(item => item !== site);
      }
    }
  }
};
</script>
<style lang="less" scoped>
.selection {
  .selection_list {
    .selection_item {
      border-radius: 8px;
      overflow: hidden;
      border: 1px solid transparent;
      .selection_checkbox {
        float: left;
        margin-left: 15px;
        margin-top: 23px;
      }
      .selection_content {
        padding: 20px 0 20px 40px;
        cursor: pointer;
        .selection_title {
          font-weight: 600;
          line-height: 25px;
          color: #333;
        }
        .selection_des {
          color: #999;
          line-height: 40px;
        }
      }
      .selection_child {
        display: none;
        line-height: 40px;
        background: #ecf0f1;
        padding-left: 40px;
      }
      &.active {
        border: 1px solid #409eff;
        .selection_child {
          display: block;
        }
      }
    }
  }
}
</style>
