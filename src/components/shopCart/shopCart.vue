<template>
    <div class="shopcart">
      <div class="content">
        <div class="content-left">
          <div class="logo-wrapper">
            <div class="logo">
              <span class="icon-shopping_cart"></span>
            </div>
          </div>

          <div class="price">{{delivery}}</div>
          <div class="desc">{{minPrice}}</div>
        </div>
        <div class="content-right"></div>
      </div>
    </div>
</template>

<script>
    export default {
        name: "shopCart",
        props:['delivery','minPrice']
    }
</script>

<style lang="stylus" scoped>

.shopcart
  position fixed
  left 0
  bottom 0
  z-index 500
  width 100%
  height 48px

  .content
    display flex
    background #141d27
    .content-left
      flex 1
      .logo-wrapper
        display inline-block
        position relative
        top -10px
        margin 0 12px
        padding 6px
        width 56px
        height 56px
        box-sizing border-box
        border-radius 50%
        background #2b243c
        .icon-shopping_cart
          line-height 44px
          font-size 24px
          color #80859a
          text-align center
      .price
        display inline-block
        vertical-align top
        margin-top 12px
        line-height 24px
        padding-right 12px
        box-sizing border-box
        border-right 1px solid rgba(255,255,255,.1)
        font-size 16px
        font-weight 700
        color rgba(255,255,255,.3)
      .desc
        display inline-block
        line-height 24px
        color rgba(255,255,255,.3)
        font-size 10px
    .content-right
      flex 0 0 105px
      width 105px

</style >
