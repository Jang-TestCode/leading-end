<template>
  <div class="footer">
    <div class="ip">
      <input type="checkbox" id="cd" :checked="isfull" @change="fullchange" />
      <label for="cd">全选</label>
    </div>
    <div class="text">
      <p>
        合计: <span>￥{{ amout }}</span>
      </p>
    </div>
    <div class="end">
      <p>结算 ({{ all }})</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    // 全选的状态
    isfull: {
      default: true,
      type: Boolean,
    },
    amout: {
      default: 0,
      type: Number,
    },
    all: {
      default: 0,
      type: Number,
    },
  },
  methods: {
    // 监听全选状态的变化
    fullchange(e) {
      this.$emit("full-change", e.target.checked);
    },
  },
};
</script>

<style lang="less" scoped>
.footer {
  height: 50px;
  padding: 5px;
  display: flex;
  justify-content: space-between;
  position: sticky;
  bottom: 0;
  background-color: white;
}
.ip {
  line-height: 45px;
}
.text {
  line-height: 45px;
}
.text span {
  font-weight: bolder;
  color: red;
}
.end {
  width: 120px;
  color: white;
  background-color: royalblue;
  line-height: 40px;
  text-align: center;
  border-radius: 30px;
}
</style>