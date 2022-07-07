<template>
  <div class="app-container">
    <!-- hearder 头部区域 -->
    <Header title="购物车"></Header>
    <!-- 循环渲染每一个商品的信息 -->
    <Goods
      class="btn1"
      v-for="item in list"
      :key="item.id"
      :id="item.id"
      :titles="item.goods_name"
      :img="item.goods_img"
      :price="item.goods_price"
      :check="item.goods_state"
      :goodscount="item.goods_count"
      @count-chang="getNewState"
    >
      <Counter
        class="btn2"
        :count="item.goods_count"
        @numup="upnum(item, $event)"
        @numdo="subnum(item, $event)"
      ></Counter>
    </Goods>
    <Footer
      :isfull="fullState"
      :amout="amt"
      :all="total"
      @full-change="getfullchange"
    ></Footer>
  </div>
</template>

<script>
// 导入 axios 请求库
import axion from "axios";
// 导入需要的组件
import Header from "@/components/Header/Header.vue";
import Goods from "@/components/Goods/Goods.vue";
import Footer from "@/components/Footer/Footer.vue";
import Counter from "@/components/Counter/Counter.vue";

export default {
  data() {
    return {
      // 用来存储购物车列表数据，默认为空数组
      list: [],
    };
  },
  components: {
    Header,
    Goods,
    Footer,
    Counter,
  },
  methods: {
    // 封装请求别数据的方法
    async initCarList() {
      // 调用 axios 的 GET 方法，请求列表数据
      const { data: res } = await axion.get("https://www.escook.cn/api/cart");
      // console.log(res);
      // 只要请求回来的数据，在页面渲染期间，则必须转存到 data 中
      if (res.status == 200) {
        this.list = res.list;
      }
    },
    // 接受子组件传递过来的参数
    getNewState(val) {
      // console.log(val);
      // 利用 some 循环，找到数组里 id 符合当前项的 id 的 列表
      this.list.some((item) => {
        if (item.id == val.id) {
          item.goods_state = val.value;
          // 循环找到对应 id 后，终止后续的循环
          return true;
        }
      });
    },
    // 接受 Footer 子组件传递过来的全选按钮的状态
    getfullchange(val) {
      // console.log(val);
      this.list.forEach((item) => (item.goods_state = val));
    },
    upnum(item, e) {
      // console.log(item, e);
      item.goods_count = e;
    },
    subnum(item, e) {
      // console.log(item, e);
      item.goods_count = e;
    },
  },
  // 计算属性
  computed: {
    // 动态计算出全选状态是 true 还是 false
    fullState() {
      return this.list.every((item) => item.goods_state === true);
    },
    // 计算已勾选商品的总价格
    amt() {
      // 1.先 filter 过滤 出已选的商品
      // 2.在 reduce 进行累加
      return this.list
        .filter((item) => item.goods_state)
        .reduce(
          (amts, item) => (amts += item.goods_price * item.goods_count),
          0
        );
    },
    // 已勾选商品的总数量
    total() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((totals, item) => (totals += item.goods_count), 0);
    },
  },
  created() {
    // 调用 axios 请求方法
    this.initCarList();
    // 根据 id 值，修改 当前的商品数
  },
};
</script>

<style lang='less' scoped>
.app-container {
  padding-top: 15px;
  padding-bottom: 20px;
}
.btn1 {
  position: relative;
}
/deep/ .btn2 {
  position: absolute;
  right: 5px;
  bottom: 0;
}
</style>