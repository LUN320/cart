<template>
  <div class="goods">
    <GoodsListitem v-for="item in goods" :key="item" :goodsitem="item"></GoodsListitem>
  </div>
</template>

<script>
import GoodsListitem from './GoodsListitem.vue'
export default {
  components:{
    GoodsListitem
  },
  props:{
    goods:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style>
.goods{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

</style>