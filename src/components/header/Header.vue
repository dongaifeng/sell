<template>
    <div class="header">
      <div class="content-wrapper">
        <div class="avatar">
          <img :src="seller.avatar" width="64px" height="64px">
        </div>

        <div class="content">
          <div class="title">
          <span class=".brand " :style="brand"></span>
            <span class="name">{{seller.name}}</span>
          </div>

          <div class="description">
                {{seller.description}}/{{seller.deliveryTime}}
          </div>
          <div v-if="seller.supports" class="support">
            <span class="icon"></span>
            <span class="text">{{seller.supports[0].description}}</span>
          </div>
        </div>

      </div>
    </div>
</template>

<script>

  export default {
    name: 'header',
    props:['seller'],
    data(){
      return {
        brand:{
          display: 'inline-block',
          width: '30px',
          height: '18px',
          backgroundImage: "url(" + require("../../../resource/img/brand@2x.png") + ")",
          backgroundRepeat: "no-repeat",
          backgroundSize: '30px 18px',
          verticalAlign: 'top'
        }
      }
    }
  }
</script>

<style scoped>
  .header{
    color:#fff;
    background: #000;

  }
  .ccontent-wrapper{
    padding: 24px 12px 18px 24px;
    font-size: 0;
  }
  .avatar{
    display: inline-block;
    vertical-align: top;
  }
  .content{
    display: inline-block;
    margin-left: 16px;
    font-size: 14px;
  }
  .title{
    margin: 2px 0 8px 0;
  }
  .brand{

  }
  .name{
    margin-left: 6px;
    font-size: 16px;
    font-weight: bold;
    line-height: 18px;
  }
  .description{
    margin-bottom: 10px;
    line-height: 12px;
    font-size: 12px;


  }
</style>
