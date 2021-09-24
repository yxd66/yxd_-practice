<template>
  <div class="list">
      <div class="cart">
          <div class="a">
              <input type="checkbox" :checked="isSelect" @click="select" ref="abc">
              <img :src="shopCart.goods_img">
          </div>
          <div class="b">
              <div>{{shopCart.goods_name}}</div>
              <div>
                  <div class="left">{{price}}</div>
                  <div class="right">
                      <button @click="lbtn" ref="lb" :disabled="isDisabled">-</button>
                      <span>{{num}}</span>
                      <button @click="rbtn" :disabled="isDisabled" ref="rb">+</button>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'Cart',
    props: ['shopCart','isAllSelect'],
    data() {
        return {
            num: 0,
            price: this.shopCart.goods_price,
            sumPrice: 0,
            isBtn: false,
            btnNum: 0
        }
    },
    methods:{
        lbtn() {
            if(this.num > 0) {
                this.num--
                this.sumPrice = this.price*this.num
                console.log(this.sumPrice)
                this.$emit('priceChange',0,this.price*-1)
            }
        },
        rbtn() {
            this.num++
            this.sumPrice = this.price*this.num
            console.log(this.sumPrice)
            this.$emit('priceChange',0,this.price)
        },
        select() {
            if (this.$refs.abc.checked) {
                this.$refs.lb.disabled = false
                this.$refs.rb.disabled = false
                this.btnNum = 1
            } else {
                this.btnNum = -1
                this.$refs.lb.disabled = true
                this.$refs.rb.disabled = true
            }
            this.$emit('priceChange',this.btnNum,this.sumPrice)
        }
    },
    computed: {
        isSelect() {
            return this.isAllSelect
        },
        isDisabled() {
            if(this.isAllSelect) {
                return false
            } else {
                return true
            }
        }
    }
}
</script>

<style scoped>
    .cart {
        height: 100px;
        display: flex;
        justify-content: space-between;
        padding: 5px;
        margin-bottom: 20px;
    }
    .a {
        height: 100%;
        display: flex;
        justify-content: space-between;
        margin-right: 10px;
    }
    .a input{
        height: 100%;
    }
    .b {
        font-size: 14px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        flex-wrap: wrap;
    }
    .b>div {
        display: flex;
        justify-content: space-between;
    }
    .b>div .left {
        color: crimson;
    }
    .b>div .right span{
        display:inline-block;
        width: 24px;
        height: 24px;
        text-align: center;
        line-height: 24px;
    }
</style>