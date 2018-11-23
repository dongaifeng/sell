<template>
  <div class="goods">
    <div class="menu-wrapper" ref="menuwrapper">
      <ul>
        <li @click="selectMenu(ind,$event)" v-for="(item,ind) in goods" class="menu-item" :class="{'current':currentIndex===ind}">
          <span class="text">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodswrapper">
      <ul>
        <li v-for="item in goods" class="food-list foodlisthook">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item">
              <div class="icon">
                <img width="57" height="57" :src="food.icon" alt="">
              </div>

              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span>月销：{{food.sellCount}}</span>
                  <span>好评率:{{food.rating}}</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>

    </div>
    <shopCart :delivery="seller.deliveryPrice" :minPrice="seller.minPrice"></shopCart>
  </div>

</template>

<script>
  import BScroll from 'better-scroll'
  import shopCart from '../shopCart/shopCart'
  export default {
    name: 'goods',
    props:['seller'],
    components:{shopCart,},
    data(){
      return {
        goods:{},
        scrollY:0,
        listHeight:[],
        classMap:['decrease','discount','special','invoice','guarantee']
      }
    },
    computed:{
      currentIndex(){
        // console.log(this.listHeight)
        for(let i=0;i<this.listHeight.length;i++){
          let height1 = this.listHeight[i];
          let height2 = this.listHeight[i+1];
          if( !height2 || (this.scrollY >= height1 && this.scrollY<height2) ){
            return i;
          }
        }
        return 0;
      }
    },
    created(){
      this.$http.get('../../../static/data.json').then((res)=>{
        this.goods = res.body.goods;
        this.$nextTick(()=>{
           this._initScroll();
           this._caluculateHeight();
        })
      });

    },
    methods:{
      _initScroll(){
        this.menuScroll = new BScroll(this.$refs.menuwrapper,{
          click:true
        })
        this.foodsScroll = new BScroll(this.$refs.foodswrapper,{
          probeType:3
        });
        this.foodsScroll.on("scroll",(pos)=>{
          this.scrollY = Math.abs(Math.round(pos.y));
        })
      },

      _caluculateHeight(){

        let foodlist = this.$refs.foodswrapper.getElementsByClassName("foodlisthook");
        // console.log(foodlist)
        let height = 0;
        this.listHeight.push(height);
        for(let i=0;i<foodlist.length;i++){
          let item = foodlist[i];
          height+=item.clientHeight;
          this.listHeight.push(height);
        }
      },
      selectMenu(ind,event){
        //console.log(ind,event);
        let foodlist = this.$refs.foodswrapper.getElementsByClassName("foodlisthook");
        this.foodsScroll.scrollToElement(foodlist[ind],500);
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>

  .goods
    display flex
    position absolute
    top 174px
    bottom 46px
    width 100%
    overflow hidden
    .menu-wrapper
      flex 0 0 80px
      background #ccc
      .menu-item
        display table
        height 54px
        width 100%
        line-height 14px
        &.current
          position relative
          z-index 222
          margin-top -1px
          background #fff
          font-weight 900
          .text
            border none
        .text
          display table-cell
          width 100%
          vertical-align middle
          font-size 12px
          border-bottom 1px solid #eee
          padding-left 10px
        .icon
          display inline-block
          vertical-align top
          width 12px
          height 12px
          margin-right 2px
          background-size 12px 12px
          background-repeat no-repeat
          &.decrease
            background-image: url("../../../resource/img/decrease_3@2x.png")
          &.discount
            background-image: url("../../../resource/img/discount_3@2x.png")
          &.special
            background-image: url("../../../resource/img/special_3@2x.png")
          &.invoice
            background-image: url("../../../resource/img/invoice_3@2x.png");
          &.guarantee
            background-image: url("../../../resource/img/guarantee_3@2x.png");
    .foods-wrapper
      flex 1
      .title
        padding-left 14px
        height 26px
        line-height 26px
        font-size 12px
        color rgb(147,153,157)
        background #f3f5f7
      .food-item
        display flex
        margin  18px
        padding-bottom 18px

        .icon
          flex 0 0 57px
          margin-right 10px
        .content
          flex 1
          .name
            margin 2px 0 6px 0
            height 14px
            line-height 14px
            font-size 14px
            color rgb(7,17,27)
          .desc, .extra
            line-height 10px
            font-size 10px
            color rgb(147,154,156)
          .desc
            margin-bottom 8px
          .extra
            .count
              margin-right 12px
          .price
            font-weight 700
            line-height 24px
            .now
              margin-right 8px
              font-size 14px
              color rgb(249,22,22)
            .old
              text-decoration line-through
              font-size 10px
              color rgb(147,155,158)




</style>

