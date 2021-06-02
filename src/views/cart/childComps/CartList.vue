<template>
  <div class="cart-list">
    <scroll :pull-up-load="true" :probe-type="3" class="content" ref="scroll">
      <li v-for="(item,index) in cartList" :key="index">
        <cart-list-item :item-info="item"></cart-list-item>
      </li>
    </scroll>
  </div>
</template>

<script>
import CartListItem from './CartListItem'
import Scroll from 'components/common/scroll/Scroll'
import { mapGetters } from 'vuex'
export default {
  name: 'CartList',
  components: {
    Scroll,
    CartListItem
  },
  computed: {
    ...mapGetters(['cartList'])
  },
  activated () {
    this.$refs.scroll.refresh()
  },
  methods: {

  }
}
</script>
<style scoped>
.cart-list {
  height: calc(100vh - 133px);
}
.content {
  height: 100%;
  overflow: hidden;
}
li {
  list-style: none;
}
</style>