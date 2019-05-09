<template>
  <div>
    <swiper v-if="imgUrls.length > 0" indidator-dots="imgUrls.length > 1">
      <block v-for="(item, index) in imgUrls" :key="index">
        <swiper-item>
          <image :src="item" mode="scaleToFill"/>
        </swiper-item>
      </block>
    </swiper>

    <div>首页</div>
  </div>
</template>

<script>
const img01 = require('@static/swiper/swiper_01.jpg')
const img02 = require('@static/swiper/swiper_02.jpg')
const img03 = require('@static/swiper/swiper_03.jpg')

export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      imgUrls: [img01, img02, img03]
    }
  },

  methods: {},

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped>
</style>
