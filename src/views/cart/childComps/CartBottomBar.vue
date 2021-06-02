<template>
  <div class="bottom-bar" v-if="cartList.length">
    <div class="check-content">
      <check-button class="check-button" :is-checked="isSelectAll" @click.native="checkClick" />
      <span>全选</span>
    </div>
    <div class="price">
      合计：￥{{totalPrice}}
    </div>
    <div class="calculate" @click="calcClick">
      去结算({{checkLength}})
    </div>
  </div>
  <div v-else class="cart-null">
    购物车空空如也，赶快去添加你喜欢的商品吧！
  </div>
</template>

<script>
import CheckButton from 'components/content/checkButton/CheckButton'
import { mapGetters } from 'vuex'
export default {
  name: 'CartBottomBar',
  components: {
    CheckButton
  },
  computed: {
    ...mapGetters(['cartList']),
    totalPrice () {
      return this.cartList.filter(item => {
        return item.checked
      }).reduce((preValue, item) => {
        return item.price * item.count + preValue
      }, 0).toFixed(2)
    },
    checkLength () {
      return this.cartList.filter(item => item.checked).length
    },
    isSelectAll () {
      //   return !(this.cartList.filter(item => !item.checked).length)
      return !this.cartList.find(item => !item.checked)
    }
  },
  methods: {
    checkClick () {
      if (this.isSelectAll) {
        this.cartList.forEach(item => item.checked = false)
      } else {
        this.cartList.forEach(item => item.checked = true)
      }
    },

    calcClick () {
      if (!this.isSelectAll) {
        this.$toast.show('请选择你要购买的商品', 2000)
      }
    }
  }
}
</script>
<style scoped>
.bottom-bar {
  height: 40px;
  background: #eee;
  position: relative;
  line-height: 40px;
  display: flex;
  font-weight: 700;
}
.check-content {
  display: flex;
  align-items: center;
}
.check-button {
  width: 20px;
  height: 20px;
  line-height: 20px;
  margin-left: 15px;
  margin-right: 5px;
}
.price {
  margin-left: 25px;
  flex: 1;
}
.calculate {
  width: 90px;
  background-color: orange;
  text-align: center;
  color: #fff;
}
.cart-null {
  position: absolute;
  font-size: 16px;
  font-weight: 700;
  text-align: center;
  height: 32px;
  top: 45px;
  left: 0;
  right: 0;
  margin-top: 20px;
}
</style>