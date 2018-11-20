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
                {{seller.description}}/{{seller.deliveryTime+"分钟送达"}}
          </div>
          <div v-if="seller.supports" class="support">
            <span class="icon" :style="icon"></span>
            <span class="text">{{seller.supports[0].description}}</span>
          </div>
        </div>
        <div v-if="seller.supports" class="support-count" @click="showDetail">
          <span class="count">{{seller.supports.length}}个</span>
          <span class="icon-keyboard_arrow_right">&gt;</span>
        </div>
      </div>
      <div class="bulletin-wrapper"  @click="showDetail">
        <span class="bulletin-title" :style="bulletinTltle"></span>
        <span class="bulletin-text">{{seller.bulletin}}</span>
        <i class="icon-keyboard_arrow_right">&gt;</i>
      </div>
      <!--背景图片-->
      <div class="bg">
        <img :src="seller.avatar" width="100%" height="100%">
      </div>
      <!--弹出层-->
      <transition name="fade">
        <div class="detail" v-show="detailShow">
          <div class="detail-wrapper clearfix">
            <div class="detail-main">
              <h1>{{seller.name}}</h1>
              <star :size="48" :score="seller.score"></star>
            </div>

            <div class="title2">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>

            <ul v-if="seller.supports" class="supports2">
              <li v-for="(item,ind) in seller.supports" class="supportLi">
                <span :class="classMap[item.type]" class="icon2"></span>
                <span class="text2">{{item.description}}</span>
              </li>
            </ul>

            <div class="title2">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>

            <div class="bulle" v-if="seller.bulletin">
              <p>{{seller.bulletin}}</p>
            </div>



          </div>
          <div class="detail-close" @click="closeDetail">
            <span>✖</span>

          </div>
        </div>
      </transition>


    </div>
</template>

<script>
import star from '../star/star'
  export default {
    name: 'myHeader',
    components:{
      star,
    },
    props:['seller'],
    methods:{
      showDetail(){
        this.detailShow = true;
      },
      closeDetail(){
        this.detailShow = false;
      }
    },
    data(){
      return {
        detailShow:false,
        classMap:['decrease','discount','special','invoice','guarantee'],
        brand:{
          display: 'inline-block',
          width: '30px',
          height: '18px',
          backgroundImage: "url(" + require("../../../resource/img/brand@2x.png") + ")",
          backgroundRepeat: "no-repeat",
          backgroundSize: '30px 18px',
          verticalAlign: 'top'
        },
        icon:{
          display: 'inline-block',
          width: '20px',
          height: '20px',
          backgroundImage: "url(" + require("../../../resource/img/decrease_4@2x.png") + ")",
          backgroundRepeat: "no-repeat",
          backgroundSize: '20px 20px',
          verticalAlign: 'middle'
        },
        bulletinTltle:{
          display: 'inline-block',
          width: '22px',
          height: '12px',
          backgroundImage: "url(" + require("../../../resource/img/bulletin@2x.png") + ")",
          backgroundRepeat: "no-repeat",
          backgroundSize: '22px 12px',
          verticalAlign: 'middle'
        }
      }
    }
  }
</script>

<style scoped>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
  .bulle{
    width: 80%;
    margin: 30px auto ;
  }
  .bulle>p{
   padding: 0 22px;
    line-height: 25px;
    font-size: 14px;
    margin-bottom: 70px;
  }
  .supports2{
    width: 80%;
    margin:0 auto 30px;
  }
  .supportLi{
    padding: 0 12px;
    margin-bottom: 12px;
    font-size: 0px;
  }
  .supportLi:last-child{
    margin-bottom: 0px;
  }
  .icon2{
    display: inline-block;
    width: 16px;
    height: 16px;
    vertical-align: top;
    background-size: 16px 16px;
    background-repeat: no-repeat;
    margin-right: 5px;
  }
  .text2{
    line-height: 18px;
    font-size: 14px;
  }
  .decrease{
    background-image: url("../../../resource/img/decrease_2@2x.png");
  }
  .discount{
    background-image: url("../../../resource/img/discount_2@2x.png");
  }
  .special{
    background-image: url("../../../resource/img/special_2@2x.png");
  }
  .invoice{
    background-image: url("../../../resource/img/invoice_2@2x.png");
  }
  .guarantee{
    background-image: url("../../../resource/img/guarantee_2@2x.png");
  }

  .title2{
    width: 80%;
    margin: 10px auto 24px;
    display: flex;
  }
  .line{
    flex: 1;
    position: relative;
    top: -6px;
    border-bottom: 1px solid rgba(255,255,255,.5);
  }
  .text{
    padding: 0 12px;
    font-size: 16px;
    font-weight: 700px !important;
  }




  .star{
    margin-top: 20px;
  }

  .clearfix{
    display: inline-block;
  }
  .clearfix:after{
    display: block;
    content: ".";
    height: 0;
    line-height: 0;
    clear: both;
    visibility: hidden;
  }
  .detail{
    position: fixed;
    top:0px;
    left:0px;
    width: 100%;
    height: 100%;
    background: rgba(7,17,27,.8);
    overflow: auto;
    z-index: 100;
    backdrop-filter: blur(10px);
  }
  .header{
    color:#fff;
    background: rgba(7,17,27,.3);
    position: relative;
    overflow: hidden;
  }
  .bg{
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    filter:blur(5px);
  }
  .content-wrapper{
    padding: 24px 12px 18px 24px;
    font-size: 0;
    position: relative;
  }
  .avatar{
    display: inline-block;
    vertical-align: top;
    /*margin:24px 16px 18px 24px;*/
    border-radius: 4px;
  }
  .content{
    display: inline-block;
    margin-left: 16px;
    font-size: 14px;
  }
  .title{
    margin: 2px 0 8px 0;
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
  .support{
    font-size: 10px;
    font-weight: 200px;
    line-height: 12px;
  }
  .support-count{
    position: absolute;
    right: 12px;
    bottom: 18px;
    padding: 0 8px;
    line-height: 24px;
    border-radius: 14px;
    background: rgba(0,0,0,0.2);
    text-align: center;
  }
  .count{
    font-size: 10px;
    vertical-align: top;
  }
  .icon-keyboard_arrow_right{
    font-size: 19px;
    color: #fff;
    vertical-align: top;
    line-height: 23px;
  }
  .bulletin-wrapper{
    height: 28px;
    line-height: 28px;
    padding: 0 22px 0 12px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    background: rgba(7,17,27,.2);
  }
  .bulletin-text{
    font-size: 10px;
    margin: 0 4px;
  }
  .detail-wrapper{
    min-height: 100%;
    width: 100%;
  }
  .detail-main{
    margin-top: 64px;
    text-align: center;
    padding-bottom: 22px;
    font-size: 22px;
  }
  .detail-close{
    position: relative;
    width: 32px;
    height: 32px;
    font-size: 32px;
    clear: both;
    margin: -64px auto 0;
  }


</style>
