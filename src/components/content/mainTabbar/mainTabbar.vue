<template>
  <div>
    <!-- <router-view></router-view> -->
    <tab-bar>
      <tab-baritme path="/home">
        <template v-slot:item-icon>
          <img src="../../../assets/img/tabbar/home.svg" alt="">
        </template>
        <template v-slot:item-icon-active>
          <img src="../../../assets/img/tabbar/home_active.svg" alt="">
        </template>
        <template v-slot:item-text>
          <div>首页</div>
        </template>
      </tab-baritme>

      <tab-baritme path="/category">
        <template v-slot:item-icon>
          <img src="../../../assets/img/tabbar/category.svg" alt="">
        </template>
        <template v-slot:item-icon-active>
          <img src="../../../assets/img/tabbar/category_active.svg" alt="">
        </template>
        <template v-slot:item-text>
          <div>分类</div>
        </template> 
      </tab-baritme>

      <tab-baritme path="/profile">
        <template v-slot:item-icon>
          <img src="../../../assets/img/tabbar/profile.svg" alt="">
        </template>
        <template v-slot:item-icon-active>
          <img src="../../../assets/img/tabbar/profile_active.svg" alt="">
        </template>
        <template v-slot:item-text>
          <div>用户</div>
        </template> 
      </tab-baritme>

      <tab-baritme path="/cart">
        <template v-slot:item-icon>
          <img src="../../../assets/img/tabbar/shopcart.svg" alt="">
        </template>
        <template v-slot:item-icon-active>
          <img src="../../../assets/img/tabbar/shopcart_active.svg" alt="">
        </template>
        <template v-slot:item-text>
          <div>购物车</div>
        </template>
      </tab-baritme>

    </tab-bar>
  </div>
</template>

<script>
import TabBar from '../../tabbar/TabBar'
import TabBaritme from '../../tabbar/TabBaritem'
export default {
  components:{
    TabBar,
    TabBaritme
  }
}
</script>

<style>

</style>