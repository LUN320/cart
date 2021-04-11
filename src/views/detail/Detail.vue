<template>
  <div class="detail4">
    <DetailNavBar class="detail-nav"/>
    <Scroll class="content" ref="srcoll">
      <DetailSwiper :topImages="topImages"></DetailSwiper>
      <DetailBaseInfo :goods="goods" /> 
      <DetailShopInfo :shop="shop"/>
      <DetailGoodsInfo :detailInfo="detailInfo" @imageLoad="imageLoad"/>
      <DetailParamInfo :paramInfo="paramInfo"/>
    </Scroll>
  </div>
  
</template>

<script>
import DetailNavBar from './chiidComps/DetailNavBar.vue'
import DetailSwiper from './chiidComps/DetailSwiper.vue'
import DetailBaseInfo from './chiidComps/DetailBaseInfo.vue'
import DetailShopInfo from './chiidComps/DetailShopInfo.vue'
import DetailGoodsInfo from './chiidComps/DetailGoodsInfo.vue'
import DetailParamInfo from './chiidComps/DetailParamInfo.vue'

import Scroll from '../../components/common/scroll/Scroll.vue'

import { getDetail,Goods,Shop,GoodsParam } from '../../network/detail.js'


export default {
  name:"Detail",
  data() {
    return {
      iid :null,
      topImages:[],
      goods:{},
      shop:{},
      detailInfo:{},
      paramInfo:{},
      commentInfo:{}
    }
  },
  components:{
    DetailNavBar,
    DetailSwiper,
    DetailBaseInfo,
    DetailShopInfo,
    DetailGoodsInfo,
    DetailParamInfo,
    Scroll,
  },

  created(){
    this.iid = this.$route.query.iid

    // 根据详情页请求数据
    getDetail(this.iid).then(res => {
      const data = res.result
      this.topImages = data.itemInfo.topImages


      //获取商品信息
      this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)

      //获取店铺信息
      this.shop  = new Shop(data.shopInfo)

      //保存商品的详细信息
      this.detailInfo = data.detailInfo;

      //参数信息
      this.paramInfo = new GoodsParam(data.itemParams.info,data.itemParams.rule);

      //评论信息
      if(data.rate.cRate !==0){
        this.commentInfo = data.rate.list[0]
      }
    })
  },
  methods:{
    imageLoad(){
      this.$refs.srcoll.refresh()
    }
  }

}
</script>

<style scoped>
.detail4{
  position: relative;
  z-index: 1;
  background-color: white;
  height: 100vh;
}
.detail-nav{
  position: relative;
  z-index: 9;
  background-color: white;
}

.content{
  /* position: absolute;
  top: 44px;
  left: 0;
  right: 0; */
  height: calc(100% - 44px);
  overflow: hidden;

}

</style>