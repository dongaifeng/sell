<template>
  <div id="app">
    <v_Header></v_Header>
   <div class="tab">
     <div class="tab-item">
       <router-link to="/goods">商品</router-link>
       </div>
     <div class="tab-item">
       <router-link to="/ratings">评论</router-link>
      </div>
     <div class="tab-item">
       <router-link to="/seller">商家</router-link>
      </div>
   </div>


    <router-view></router-view>
  </div>
</template>

<script>
  import Header from './components/header/Header'
export default {
  name: 'App',
  components:{
    'v_Header':Header,
  }
}
</script>

<style>
  #app .tab{
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
  }
  .tab-item{
    flex: 1;
    text-align: center;
  }

</style>
