<template>
    <div class="star" :class="starType">
      <span v-for="itemClass in itemClasses" :class="itemClass" class="star-item">

      </span>
    </div>
</template>

<script>
  const LENGTH = 5;
  const CLS_ON = 'on';
  const CLS_HALF = "harf";
  const CLS_OFF = 'off';
  export default {
    name: "star",
    props:["size","score"],
    computed: {
      starType(){
        console.log(this.size);
        return 'star-'+ this.size
      },
      itemClasses(){
        console.log(this.score);
        let result = []
        let score = Math.floor(this.score * 2) / 2
        let hasDecimal = score % 1 !== 0;
        let integer =Math.floor(score);
        for(let i =0;i<integer;i++){
          result.push(CLS_ON);
        };
        if(hasDecimal){
          result.push(CLS_HALF)
        }
        while(result.length<LENGTH){
          result.push(CLS_OFF)
        }

        console.log(result)
        return result

      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .star
    font-size 0
    .star-item
      display inline-block
      background-repeat no-repeat
    &.star-48
      .star-item
        width 20px
        height 20px
        margin-right 22px
        background-size 20px 20px
        &.on
          bg-img('star48_on')
        &.harf
          bg-img('star48_half')
        &.off
          background-image url("./star48_off@2x.png")
    &.star-36
      width 15px
      height 15px
      margin-right 6px
      background-size 15px 15px
      &.on
        bg-img('star36_on')
      &.harf
        bg-img('star36_half')
      &.off
        bg-img('star36_off')
    &.star-24
      width 10px
      height 10px
      margin-right 3px
      background-size 10px 10px
      &.on
        bg-img('star24_on')
      &.harf
        bg-img('star24_half')
      &.off
        bg-img('star24_off')


</style>
