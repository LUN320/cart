<template>
  <div class="nav-bar">
    <div class="left"><slot name="left"></slot></div>
    <div class="center"><slot name="center"></slot></div>
    <div class="right"><slot name="right"></slot></div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.nav-bar{
  display: flex;
  height: 44px;
  width: 100%;
  line-height: 44px;
  text-align: center;
}

.left , .right{
  width: 44px;
}

.center{
  flex: 1;
}

</style>