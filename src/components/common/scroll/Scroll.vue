<template>
  <div class="wrapper2" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import Scroll from 'better-scroll'
export default {
  props:{
    probeType:{
      type:Number,
      default:0
    },
    pullUpLoad:{
      type:Boolean,
      default:false
    }
  },
  data() {
    return {
      scroll :null
    }
  },
  mounted() {
    // 创建Bscroll对象
    this.scroll = new Scroll(this.$refs.wrapper,{
      probeType:this.probeType,
      pullUpLoad:this.pullUpLoad,
      click:true,
      mouseWheel:true,
      observeDOM:true
    })

    //创建监听滚动监听
    if(this.probeType===2 || this.probeType===3){
      this.scroll.on('scroll',(position) =>{
      this.$emit('scroll',position)
      })
    }

    //监听上拉加载更多事件
    if(this.pullUpLoad){
      this.scroll.on('pullingUp',()=>{
      this.$emit('pullingUp')
      })
    }
    
  },

  methods:{
    finishPullUp(){
      this.scroll && this.scroll.finishPullUp();
    },
    refresh(){
      this.scroll && this.scroll.refresh();
    }

  }


}
</script>

<style>

</style>