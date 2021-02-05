<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page, index) of pages" :key="index" >
        <div class="icon"
             v-for="item of page"
             :key="item.id"
        >
          <div class="icon-img">
            <img class="icon-img-content" :src="item.imgUrl" />
          </div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  data () {
    return {
      swiperOption: {
        loop: false,
        autoplay:false
      }
    }
  },
  props:{
    list:Array
  },
  computed: {
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        // 假设为第三个数据，则对应index为2，2/8向下取整为0，代表数据在第1页
        const page = Math.floor(index / 8)
        if (!pages[page]) { // 当page为0时，由于pages是空数组，所有pages[0]没有内容,那么将其赋值为空数组
          pages[page] = [] // pages[0]=[]
        }
        pages[page].push(item) // 将元素追加到pages[0]这个数组中，追加之后pages:[[item]]
      })
      return pages // [[最多8个元素],[]]
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  @import '~styles/mixins.styl'
  .icons >>> .swiper-container
    height:0
    padding-bottom:50%
  .icon
      position: relative
      overflow: hidden
      width:25%
      height: 0
      padding-bottom: 25%
      float: left
      .icon-img
        position :absolute
        top: 0
        left: 0
        right: 0
        bottom: .44rem
        box-sizing: border-box
        padding: .1rem
      .icon-img-content
          display :block
          margin: 0 auto
          height: 100%
      .icon-desc
        position :absolute
        left :0
        right: 0
        bottom: 0
        height: .44rem
        line-height: .44rem
        color:$darkTextColor
        text-align center
        ellipsis()
</style>
