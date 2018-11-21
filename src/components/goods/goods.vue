<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="item in goods" class="menu-item">
          <span class="text">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper"></div>
  </div>

</template>

<script>
  export default {
    name: 'goods',
    props:['seller'],
    data(){
      return {
        goods:{},
        classMap:['decrease','discount','special','invoice','guarantee']
      }
    },
    created(){
      this.$http.get('../../../static/data.json').then((res)=>{
        console.log(res)
        this.goods = res.body.goods
      })
    },
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
      background #f3f5f7
      .menu-item
        display table
        height 54px
        width 100%
        line-height 14px
        .text
          display table-cell
          width 100%
          vertical-align middle
          font-size 12px
          border-bottom 1px solid rgba(7,17,27,.3)
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



</style>

