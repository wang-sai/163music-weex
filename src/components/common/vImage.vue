<template>
  <image :src="locationSrc"></image>
</template>

<script>
// import { getPlatform, getHost } from '@/common/js/util'
import { getHost } from '@/common/js/util'

export default {
  name: 'image',
  props: {
    src: {
      type: String,
      default: ''
    }
  },
  computed: {
    locationSrc () {
      return this.setImageUrl(this.src)
    }
  },
  methods: {
    setImageUrl (src) {
      return {
        /**
         * Android本地路径
         * 对应src -> main -> assets -> images(自己新建的文件夹)
         */
        android: `file:///android_asset/images/${src}`,
        /**
         * IOS本地路径
         * 对应 WeexDemo.xcworkspace(xcode打开)
         * WeexDemo ->resource -> images(xcode不会自动添加图片，需手动添加)
         */
        ios: `local:///images/${src}`,
        web: this.webUrl(src)
      // }[getPlatform()]
      }['web']
    },
    webUrl (src) {
      if (src.indexOf('http') >= 0) {
        return src
      }
      // return `http://192.168.1.11:8081/src/assets/images/${src}` // for test
      // return `${getHost()}/src/assets/images/${src}`
      return `${getHost()}/163music-weex/src/assets/images/${src}`
    }
  }
}
</script>

<style scoped>
</style>
