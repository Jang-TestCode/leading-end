<template>
  <div class="goods">
    <!-- 复选框区域 -->
    <div class="ip">
      <input
        type="checkbox"
        :checked="check"
        :id="'cd' + id"
        @change="stateChange"
      /><!-- change 事件是复选框本身就有的事件 -->
    </div>
    <!-- 图片区域 -->
    <div class="pic">
      <!-- label 可以通过 for 属性点击到 input  -->
      <label :for="'cd' + id"><img :src="img" alt="" /></label>
    </div>
    <!-- 标题区域 -->
    <div class="text">
      <p>{{ titles }}</p>
      <!-- 价格 -->
      <p class="bo">￥{{ price }}</p>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    // 商品的id
    // 为啥这里要封装一个id属性呢？
    // 原因：将来子组件中的商品的勾选状态变化之后，需要通过子传父的方式 通知父组件 根据 id 修改对应商品的勾选给状态
    id: {
      required: true,
      type: Number,
    },
    // 要渲染的商品标题
    titles: {
      default: "",
      type: String,
    },
    // 要渲染的商品图片
    img: {
      default: "",
      type: String,
    },
    // 要渲染商品的单价
    price: {
      default: 0,
      type: Number,
    },
    // 商品的勾选状态
    check: {
      default: true,
      type: Boolean,
    },
    goodscount: {
      default: 1,
      type: Number,
    },
  },
  data() {
    return {};
  },
  methods: {
    // 只要复选框的选中状态发生了变化，就会调用这个处理函数
    stateChange(e) {
      // 通过 e 事件对象 可以拿到 复选框的最新勾选状态
      const newstate = e.target.checked;
      // 触发自定义事件
      // 传递两个参数，当前的id 和 最新勾选状态
      this.$emit("count-chang", { id: this.id, value: newstate });
    },
  },
};
</script>

<style lang="less" scoped>
.goods {
  height: 149px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.3);
  display: flex;
  padding: 5px 5px 4px;
}
.ip {
  align-self: center;
  padding: 5px 5px 4px;
}
.pic {
  padding: 5px 5px 4px;
}
.text {
  flex: 1;
  position: relative;
  font-weight: bold;
  padding: 5px 5px 4px;
}
.bo {
  position: absolute;
  color: red;
  bottom: 0;
}
</style>