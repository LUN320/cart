<template>
    <Swiper class="swiper">
      <SwiperItem v-for="(item,index) in banners" :key="index">
        <a :href="item.link"><img :src="item.image" alt="" @load="imgesLoad"></a>
      </SwiperItem>
    </Swiper>
</template>

<script>
import {Swiper, SwiperItem} from '../../../components/common/swiper/index.js'
export default {
  props:{
    banners:{
      type:Array,
      default(){
        return []
      }
    }
  },
  data() {
    return {
      isLoad:false,
    }
  },
  components:{
    Swiper,
    SwiperItem,
  },
  methods:{
    imgesLoad(){
      if(!this.isLoad){
        this.$emit('swiperImgesLoad')
        this.isLoad =true
      }
      
    }
  }
}
</script>

<style>
</style>