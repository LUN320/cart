<template>
  <div>分类</div>
</template>

<script>
import Bscroll  from 'better-scroll'
export default {
  data() {
    return {
      scrool :null
    }
  },
  mounted(){
    this.scrool = new Bscroll(document.querySelector('.wrapper'),{
       
    })
  }
}
</script>

<style scope>
/* .wrapper{
  height: 150px;
  background-color: red;
  overflow-x: hidden;

  overflow-y: scroll;
} */
</style>