<template>
  <div class="counter">
    <!-- 减一按钮 -->
    <button @click="sub">-</button>
    <!-- 商品购买的数量 -->
    <span> {{ count }} </span>
    <!-- 加一按钮 -->
    <button @click="add">+</button>
  </div>
</template>

<script>
export default {
  props: {
    // 接受商品的 id 值，将来使用 EventBus 方案，把数量传递到 App.vue 的时候，
    // 通知 App.vue，需要更行哪一个商品的数量

    // 接受到的商品数量值
    count: {
      default: 1,
      type: Number,
    },
  },

  methods: {
    // 点击按钮，数值 +1
    add() {
      this.$emit("numup", this.count + 1);
    },
    sub() {
      // 需要加个判断，减到 0 的时候，终止
      if (this.count - 1 === 0) return;
      this.$emit("numdo", this.count - 1);
    },
  },
};
</script>

<style lang="less" scoped>
.counter {
  padding: 0;
  margin: 0;
  font-weight: bold;
  text-align: center;
}
.counter button {
  width: 25px;
  height: 25px;
  margin-right: 10px;
  border: 0;
}
.counter span {
  margin-right: 10px;
}
.counter button:last-child {
  margin-right: 0;
}
</style>