<template lang="pug">
.overlay
  .overlay_transition
  .overlay_item(v-for="(article, a_id) in articlesData"
                :id="'preview-' + (a_id + 1)")
    .thumbnail_box
      .thumbnail_shadow
      img.thumbnail_img.original(:src="article.coverImg")
    .article_box
      .headline_box
        .tag 【 {{ article.tag[0] }} 】
        .title {{ article.title }}
        .publisher
          .author by {{ article.author }}
          .date {{ article.date }}
      ContentBox(:article_id="a_id")
      .detail_box
        .infomation
          h5 店家地址
          h4 {{ article.detail[0] }}
          h5 營業時間
          h4 {{ article.detail[1] }}
          h5 網站 / 臉書粉絲專頁
          a.btn_fb(:href="article.detail[2]"
                    target="_blank")
            i.fab.fa-facebook-f
        .map
          iframe(:src="article.detail[3]"
                  frameborder="0"
                  allowfullscreen)
  Cross
</template>

<script>
import { mapState } from 'vuex'
import ContentBox from '@/components/ContentBox'
import Cross from '@/components/Cross'

export default {
  components: {
    ContentBox, Cross
  },
  computed: {
    ...mapState(['articlesData'])
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.overlay
  +size(100%)
  position: fixed
  top: 0
  left: 0
  z-index: 1000
  overflow: scroll
  pointer-events: none
  &.overlay_opened
    pointer-events: auto
  .overlay_transition
    +size(100%, 20000px)
    background-color: black
    position: absolute
    top: 0
    left: 0
    z-index: 100
    transform: translate3d(100%, 0, 0)
  .overlay_item
    +size(100%)
    padding: 5rem 5vw
    background-color: $c_white
    position: absolute
    top: 0
    left: 0
    +center_flex(center, flex-start)
    flex-direction: column
    opacity: 0
    .thumbnail_box
      max-width: 600px
      max-height: 100%
      margin: 5vw 0 0 0
      .original
        max-height: calc(100vh - 20rem)
        filter: none
    .article_box
      max-width: 33rem
      margin: 1rem 3vw 0 9vw
      +center_flex
      flex-direction: column
      .headline_box
        max-width: 600px
        margin: 5vw 0
        .tag
          padding: 0 0 50px 0
          font-size: 1.2rem
          font-weight: 300
          color: $c_black
        .title
          padding: 0 0 120px 0
          font-size: 1.6rem
          font-weight: 500
        .publisher
          +center_flex(flex-end)
          .author, .date
            padding: 0 20px 0 0
            font-size: 0.9rem
            font-weight: 300
            color: rgba($c_black, 0.5)
      .detail_box
        +size(100%)
        +center_flex
        flex-direction: column
        .infomation
          margin: 50px 0
          +center_flex(center, flex-start)
          flex-direction: column
          h5
            margin: 10px 0
            border-bottom: 1px solid $c_black
            font-size: 1rem
            color: $c_black
          h4
            font-size: 1rem
            font-weight: 300
            color: $c_black
          .btn_fb
            +size(25px, 25px, 8px)
            border: 1px solid $c_blue
            text-decoration: none
            +center_flex
            transition: 0.8s
            &:hover
              background-color: $c_blue
              i
                color: white
            i
              padding: 0 0 0 2px
              font-size: 0.9rem
              color: $c_blue
        .map
          margin: 50px 0
          iframe
            +size(40vw, 35vw)
            max-width: 500px
            max-height: 450px

// ====================
//      RWD
// ==============================

// --------------------
//      MEDIUM_DESKTOP
// ------------------------------
@media screen and (min-width: 880px)
  .overlay
    .overlay_item
      flex-direction: row

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  .overlay
    // -webkit-overflow-scrolling: touch
    .overlay_item
      .thumbnail_box
        position: absolute
        top: 10%
        left: 10%
      .article_box
        margin: 0
        padding: 0 8vw
        position: absolute
        top: 60%
        left: 0
        .detail_box
          .map
            margin: 25px 0 50px 0
            iframe
              +size(17rem)
</style>
