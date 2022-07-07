<template>
  <div class="header">{{ title }}</div>
</template>

<script>
export default {
  props: {
    title: {
      default: "",
      type: String,
    },
  },
  data() {
    return {};
  },
  methods: {},
};
</script>

<style lang='less' scoped>
.header {
  font-size: 12px;
  height: 45px;
  width: 100%;
  text-align: center;
  line-height: 45px;
  background-color: dodgerblue;
  color: aliceblue;
}
</style>