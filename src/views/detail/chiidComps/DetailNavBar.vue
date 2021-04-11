<template>
  <div>
    <NavBar>
      <template v-slot:left>
        <div class="back" @click="backCliclk">
          <img src="../../../assets/img/common/back.svg" alt="">
       </div>
      </template>

      <template v-slot:center>
        <div class="title">
          <div v-for="(item,index) in title" :key="index"
         class="title-item"
         :class="{active:currentIndex===index}"
         @click="titleClick(index)">{{item}}</div>
        </div>
      </template>

    </NavBar>
  </div>
</template>

<script>
import NavBar from '../../../components/common/navbar/NavBar.vue'
export default {
  data() {
    return {
      title:['商品','参数','评论','推荐'],
      currentIndex :0
    }
  },
  components:{
    NavBar
  },
  methods:{
    titleClick(index){
      this.currentIndex = index
    },
    backCliclk(){
      this.$router.back()
    }

  }
}
</script>

<style scopde>
.title{
  display: flex;
  font-size: 13px;
}
.title-item{
  flex: 1;
}
.active{
  color: palevioletred;
}

.back img{
  margin-top: 10px;
}

</style>