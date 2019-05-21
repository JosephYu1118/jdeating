<template lang="pug">
.content_box(v-html="getContent(articlesData[article_id].content)")
</template>

<script>
import { mapState } from 'vuex'

export default {
  props: [
    'article_id'
  ],
  computed: {
    ...mapState(['articlesData'])
  },
  methods: {
    getContent (contentData) {
      let contentHtml = ``
      contentData.forEach(item => {
        if (item.indexOf('NT$') !== -1) {
          contentHtml += `<h6>${item}</h6>`
        } else if (item.indexOf('/') === 0) {
          let imgUrl = require('@/assets' + item)
          contentHtml += `<img src='${imgUrl}'>`
        } else {
          contentHtml += `<p>${item}</p>`
        }
      })
      return contentHtml
    }
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.content_box
  +center_flex
  flex-direction: column
  img
    width: 90%
    max-width: 700px
    min-width: 350px
    padding: 20px 0
  p
    max-width: 800px
    min-width: 250px
    padding: 20px 0
    text-indent: 35px
    font-size: 1rem
    font-weight: 300
    line-height: 180%
  h6
    padding: 10px 0
    font-size: 1rem

// ====================
//      RWD
// ==============================

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  .content_box
    img
      width: 90%
      min-width: 250px
      padding: 20px 0
    p
      min-width: 150px
      padding: 20px 0
      text-indent: 35px
      font-size: 1rem
      font-weight: 300
      line-height: 180%
</style>
