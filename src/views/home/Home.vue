<template>
  <div id="home">
    <Nav-Bar class="home-nav">
      <template v-slot:center>
        <div>购物街</div>
      </template>
      
    </Nav-Bar>

    <TabControl :title="['流行','新款','精选']"
       @tabClick="tabClick" 
       ref="tabControl1" class="tab-control" v-show="isTabFixed"></TabControl>
    
    <Scroll class="content2" ref="scroll" 
    :probe-type="3" 
    @scroll="scrollBackTop"
    :pull-up-load="true"
    @pullingUp="loadMore">
      <Home-Swper :banners="banners" @swiperImgesLoad="swiperImgesLoad"></Home-Swper>
      <Rencommend-View :recommends="recommends"></Rencommend-View>
      <FestureView/>
      <TabControl :title="['流行','新款','精选']"
       @tabClick="tabClick" 
       ref="tabControl2"></TabControl>
      <GoodsList :goods="showgoods"></GoodsList>
    </Scroll>

    <BackTop @click="backClick" v-show="isShowBackTop"></BackTop>
    
    <!-- <List/> -->
  </div>
</template>

<script>
import NavBar from '../../components/common/navbar/NavBar.vue';
import HomeSwper from './chiidComps/HomeSwper.vue';
import RencommendView from './chiidComps/RencommendView.vue';
import FestureView from './chiidComps/FeatureView.vue';
import GoodsList from '../../components/content/goods/GoodsList.vue'
import Scroll from '../../components/common/scroll/Scroll.vue'
import BackTop from '../../components/content/backTop/BackTop.vue'

// import List from './chiidComps/List';

import TabControl from '../../components/content/TabControl/TabControl.vue'

import {getHomeMultidata , getHomeGoods} from '../../network/home.js';

export default {
  components:{
    NavBar,
    HomeSwper,
    RencommendView,
    FestureView,
    TabControl,
    GoodsList,
    Scroll,
    BackTop
    // List
  },
  data() {
    return {
      banners:[],
      recommends:[],
      goods:{
        'pop':{page:0,list:[]},
        'sell':{page:0,list:[]},
        'new':{page:0,list:[]},
      },
      currentType:'pop',
      isShowBackTop:false,
      tabOffsetTop:0,
      isTabFixed:false,
      saveY:0
    }
  },
  activated(){
    this.$refs.scroll.scroll.scrollTo(0,this.saveY,0);
    this.$refs.scroll.refresh()
  },
  deactivated(){
    this.saveY = this.$refs.scroll.scroll.y
  },
  created(){
    //轮播图数据请求
    this.getHomeMultidata()

    //列表数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')

    //监听item图片加载完成
    // this.$bus.$on('itemImgesLoad',()=>{
    //   console.log('------');
    // })
  },
  methods:{
    //事件监听相关方法
    tabClick(index){
      switch (index){
        case 0 :
          this.currentType ='pop'
          break
        case 1 :
          this.currentType ='new'
          break
        case 2 :
          this.currentType ='sell'
          break
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },
    backClick(){
      this.$refs.scroll.scroll.scrollTo(0,0,500)
    },

    //回到顶部
    scrollBackTop(position){
      this.isShowBackTop = (-position.y) > 900
      this.isTabFixed = (-position.y) >this.tabOffsetTop
    },

    //上拉加载
    loadMore(){
      this.getHomeGoods(this.currentType)
    },

    swiperImgesLoad(){
      this.tabOffsetTop =this.$refs.tabControl2.$el.offsetTop
    },


    // 网络请求相关方法
    getHomeMultidata(){
      getHomeMultidata().then(res =>{
      this.banners = res.data.banner.list
       this.recommends = res.data.recommend.list
      // console.log('aaa');
      })
    },
    getHomeGoods(type){
      const page = this.goods[type].page + 1
      getHomeGoods(type,page).then(res =>{
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1

        this.$refs.scroll.finishPullUp()
      })
    }
  },
  computed:{
    showgoods(){
      return this.goods[this.currentType].list
    }
  }
}
</script>

<style scoped>

#home{
  /* padding-top: 44px; */
  height: 100vh;
  position: relative;
}

.home-nav{
  width: 100%;
  background-color: pink;
  color: #fff;
  /* position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 9; */
}

/* .tab-control{
  position: sticky;
  top:44px;
  z-index: 9;
} */

.content2{
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}

/* .content2{
  height: calc(100% - 93px);
  overflow: hidden;
} */

.tab-control{
  position: relative;
  z-index: 9;
}

</style>