<template>
  <div class="ducascader">
    <cascader-panel
      :options="options"
      v-model="checkedValue"
      :setting="setting"
      @nodes="changeNodes"
      :props="props"
    ></cascader-panel>
  </div>
</template>

<script>
import cascaderPanel from "@/components/cascader-panel/cascader-panel";
const calcValueToZip = node => {
  if (node.checked) {
    return [node.value];
  }
  if (!node.children.length) {
    return [];
  }
  return node.children
    .map(CN => calcValueToZip(CN))
    .filter(CN => CN)
    .reduce((tot, CN) => tot.concat(CN));
};
export default {
  components: { cascaderPanel },
  props: ["options", "value", "setting", "iszip", "props"],
  data() {
    return {
      valueByOptions: []
    };
  },
  computed: {
    checkedValue: {
      get() {
        return this.valueByOptions.filter(
          item => item.filter(ci => this.value.indexOf(ci) > -1).length
        );
      },
      set(val) {
        if (this.iszip) {
          val = this.nodes
            .map(node => calcValueToZip(node))
            .reduce((tot, CN) => tot.concat(CN));
        } else {
          val = val.map(item => item[item.length - 1]);
        }
        this.$emit("input", val);
      }
    }
  },
  methods: {
    changeNodes(nodes) {
      this.nodes = nodes;
    },
    tranOption(item, res = []) {
      res.push(item[this.props.value]);
      if (item[this.props.children] && item[this.props.children].length) {
        return item[this.props.children].map(CN =>
          this.tranOption(CN, [].concat(res))
        );
      }
      this.valueByOptions.push(res);
    }
  },
  created() {
    this.options.map(item => this.tranOption(item));
  },
  watch: {
    options() {
      this.options.map(item => this.tranOption(item));
    }
  }
};
</script>

<style>
</style>