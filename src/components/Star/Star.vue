<template>
  <div class="star" :class="'Star-'+ size">
    <!--<span class="Star-item on"></span>-->
    <!--<span class="Star-item on"></span>-->
    <!--<span class="Star-item on"></span>-->
    <!--<span class="Star-item half"></span>-->
    <!--定义一个数组，on，half，off-->
    <span class="star-item" v-for="(sc,index) in starClasses" :key="index" :class="sc"></span>

  </div>
</template>

<script>
  export default {
    props: {
      score: Number,
      size: Number
    },
    computed: {
      starClasses() {
        /*通过score计算on half off的个数
        1. on为score的整数，用Math.floor(score)
        2. half为0或1（小数大于等于0.5）个，小数允许不精确，x10变成整数
        3. 剩下的off用while循环加到数组的length为5*/

        const {score} = this
        const scs = []
        const scoreInteger = Math.floor(score)
        for (let i = 0; i < scoreInteger; i++) {
          scs.push('on')
        }
        if ((score - scoreInteger) * 10 >= 5) {
          scs.push('half')
        }
        while (scs.length < 5) {
          scs.push('off')
        }
        return scs
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixins.styl'
  .star // 2x图 3x图
    float left
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

        &:last-child
          margin-right 0

        &.on
          bg-image('./images/star48_on')

        &.half
          bg-image('./images/star48_half')

        &.off
          bg-image('./images/star48_off')

    &.star-36
      .star-item
        width 15px
        height 15px
        margin-right 6px
        background-size 15px 15px

        &:last-child
          margin-right 0

        &.on
          bg-image('./images/star36_on')

        &.half
          bg-image('./images/star36_half')

        &.off
          bg-image('./images/star36_off')

    &.star-24
      .star-item
        width 10px
        height 10px
        margin-right 3px
        background-size 10px 10px

        &:last-child
          margin-right 0

        &.on
          bg-image('./images/star24_on')

        &.half
          bg-image('./images/star24_half')

        &.off
          bg-image('./images/star24_off')

</style>
