<template>
  <div class="detail">
    <Swiper class="swiper">
      <SwiperItem v-for="item in topImages" :key="item">
        <img :src="item" alt="">
      </SwiperItem>
    </Swiper>
  </div>
</template>

<script>
import Swiper from '../../../components/common/swiper/Swiper.vue'
import SwiperItem from '../../../components/common/swiper/SwiperItem.vue'
export default {
  props:{
    topImages:{
      type:Array,
      default(){
        return []
      }
    }
  },
comments:{
  Swiper,
  SwiperItem
}
}
</script>

<style>
.detail{
  height: 300px;
  overflow: hidden;
}

</style>