<template>
  <div class="rencomend">
    <div v-for="item,index in recommends" :key="index" class="rencomend_img">
      <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    recommends:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style>
  .rencomend{
    display: flex;
    width: 100%;
    justify-content: space-around;
    text-align: center;
    font-size: 14px;
    padding: 10px 0 20px;
    border-bottom: solid 8px #eee;
  }

  .rencomend_img{
    flex: 1;
  }

  .rencomend_img a{
    color: gray;
    text-decoration: none;
    
  }

  .rencomend_img img{
    width: 75%;
    height: 75%;
    margin-bottom: 15px;
  }


</style>