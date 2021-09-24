<template>
  <div id="app">
    <div class="header">
      <div>购物车案例</div>
    </div>
    <cart v-for="(item,index) in shopCart" :key="item.index" :shopCart="shopCart[index]" :isAllSelect="isAllSelect" @priceChange="_priceChange"></cart>
    <footer>
      <div class="allClick">
        <input type="checkbox" @click="allSelect">全选
      </div>
      <div class="sum">合计：<span>{{allPrice}}</span></div>
      <div class="butn">
        <div>结算（{{btns}}）</div>
      </div>
    </footer>
  </div>
</template>

<script>
var axios = require("../axios.js");
import Cart from "@/components/Cart.vue";
export default {
  name: "App",
  components: {
    Cart,
  },
  data() {
    return {
      shopCart: [],
      isAllSelect: false,
      allPrice: 0,
      btns: 0
    }
  },
  methods: {
    allSelect() {
      this.isAllSelect = !this.isAllSelect
      this.isAllSelect ? this.btns=this.shopCart.length : this.btns=0
      if(this.isAllSelect == false) {
        this.allPrice = 0
      }
    },
    _priceChange(num1,num2) {
        this.btns += num1
        this.allPrice += num2
    }
  },
  created() {
    axios({
      url: "https://www.escook.cn/api/cart",
      method: "get",
    }).then((res) => {
      var a = res.data.list
      this.shopCart = a
      console.log(a)
    });
  },
};
</script>

<style lang="less">
#app {
  padding-bottom: 40px;
}
body {
  width: 100%;
  margin: 0;
}
.header {
  width: 100%;
  height: 50px;
  text-align: center;
  margin-bottom: 10px;
  background-color: dodgerblue;
}
.header div {
  line-height: 50px;
  color: white;
}
footer {
  height: 50px;
  line-height: 50px;
  position: fixed;
  background-color: white;
  bottom:0;
  display: flex;
  justify-content: space-between;
}
.allclick{
  position: relative;
}
.sum{
  position: relative;
  left: 50px;
}
.sum span {
  color:crimson
}
.butn{
  position: relative;
  left: 120px;
  
}
.butn div {
  background-color:dodgerblue;
}
</style>
