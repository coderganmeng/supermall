<!--  -->
<template>
  <div class="recommend">
    <div class="recommend-item" v-for="item in recommends">
      <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>

export default {
  name: 'RecommendView',
  props: {
    recommends: {
      type: Array,
      default () {
        return []
      }
    }
  }
}
</script>
<style scoped>
.recommend {
  display: flex;
  text-align: center;
  padding: 10px 0px 20px;
  border-bottom: solid 10px #eee;
}
.recommend-item {
  flex: 1;
}
.recommend-item img {
  width: 78px;
  height: 78px;
  margin-bottom: 8px;
}
</style>