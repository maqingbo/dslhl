<template>
  <div class="container">
    <swiper
      class="swiper"
      indicator-dots="true"
      circular="true"
      bindchange="bindchange"
      :style="{height: imgsHeight[current] + 'px'}"
    >
      <block v-for="(item, index) in imgUrls" :key="index">
        <swiper-item class="swiper_item">
          <image
            :src="item.url"
            class="slide_image"
            :data-id="index"
            mode="aspectFill"
            bindload="imageLoad"/>
        </swiper-item>
      </block>
    </swiper>

    <div>首页</div>
  </div>
</template>

<script>
import {api} from '@/api'

export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      windowWidth: 0,
      windowHeight: 0,
      imgUrls: api.home.swiperImgs,
      imgsHeight: []
    }
  },
  computed: {
    // 以最高图片的高度作为 swiper 的高度
    swiperHeight () {
      return Math.max(...this.imgsHeight)
    }
  },
  methods: {
    // 每张图片加载完成会执行 imageload 方法
    imageLoad: function (e) {
      // 获取图片宽高比
      const ratio = e.detail.width / e.detail.height
      // 按照宽高比计算图片宽度 100% 时的高度
      const imgHeight = this.windowWidth / ratio
      // 把每一张图片对应的高度记录到 imgsHeight 数组里
      this.imgsHeight[e.target.dataset.id] = imgHeight
      // console.log(this.imgsHeight)
    }
  },
  created () {
    // 获取设备屏幕尺寸
    wx.getSystemInfo({
      success: res => {
        this.windowWidth = res.windowWidth
        this.windowHeight = res.windowHeight
      }
    })
  }
}
</script>

<style scoped lang="scss">
.container {
  position: fixed;
  width: 100%;
  height: 100%;
  .swiper {
    width: 100%;
    background-color: skyblue;
    .swiper_item {
      image {
        width: 100%;
        height: 100%;
      }
    }
  }
}
</style>
