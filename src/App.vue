<template>
  <div id="app">
    <router-view v-slot="{ Component }">
      <keep-alive exclude="Detail">
        <component :is="Component" />
      </keep-alive>
    </router-view>
    <main-tabbar/>
  </div>
</template>
<script>
import MainTabbar from './components/content/mainTabbar/mainTabbar.vue'

export default {
  components:{
    MainTabbar
  }
  
}
</script>

<style scopes>
@import './assets/css/base.css';
</style>
