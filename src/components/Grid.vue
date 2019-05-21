<template lang="pug">
.grid
  a.grid_item(v-for="(article, a_id) in articlesData"
              :href="'#preview-' + (a_id + 1)")
    .thumbnail_box
      .thumbnail_shadow
      img.thumbnail_img(:src="article.coverImg")
      h3.article_title
        .title_inner(:data-hover="article.title.split(' — ')[1]") {{ article.title.split(" — ")[1] }}
      h4.article_description
        .description_inner(:class="getTextStyle()") {{ article.title.split(" — ")[0] }}
</template>

<script>
import { mapState } from 'vuex'

let order = [1, 2, 3]

export default {
  computed: {
    ...mapState(['articlesData'])
  },
  methods: {
    getTextStyle () {
      let blackBox = Math.random() > 0.5 ? 'inner_black ' : ''
      if (order.length === 0) {
        order = [1, 2, 3]
      }
      order.sort((a, b) => Math.random() > 0.5 ? 1 : -1)
      return blackBox + 'rotate_0' + order.pop()
    }
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.preview_opened
  overflow: hidden

.grid
  width: 100%
  max-width: 1440px
  margin: 0 auto
  padding: 0 0 10rem 0
  .grid_item
    margin: 0 0 10rem 0
    padding: 0 0 3rem 0
    text-decoration: none
    color: black
    +center_flex
    cursor: pointer
    outline: none
    &:hover, &:focus
      color: black
      outline: none
    &:hover
      .thumbnail_box
        .thumbnail_img:not(.original)
          filter: grayscale(0)
        .article_title
          .title_inner
            &:before
              +size(100%)

.thumbnail_box
  margin: 2rem
  .thumbnail_shadow
    +size(100%)
    background-image: linear-gradient(135deg, transparent 47%, black 47%, black 52%, transparent 52%)
    background-size: 10px 10px
    position: absolute
    top: -1rem
    left: -1rem
  .thumbnail_img
    max-width: 90%
    flex: none
    margin: 0 auto
    display: block
    pointer-events: none
    filter: grayscale(1)
    transition: filter 0.3s
  .article_title
    margin: 0
    position: absolute
    z-index: 1
    .title_inner
      font-size: 1.2rem
      display: block
      &[data-hover]
        -webkit-text-stroke: 0.5px rgba(black, 0.3)
        text-stroke: 0.5px rgba(black, 0.3)
        -webkit-text-fill-color: transparent
        text-fill-color: transparent
        color: transparent
      &:before
        height: 0
        content: attr(data-hover)
        -webkit-text-stroke: 0
        text-stroke: 0
        -webkit-text-fill-color: #000
        text-fill-color: #000
        color: #000
        position: absolute
        top: 0
        left: 0
        white-space: nowrap
        overflow: hidden
        transition: all 0.3s
  .article_description
    margin: 0.5rem 1rem
    font-size: 0.8rem
    font-weight: 700
    position: absolute
    top: -5rem
    .description_inner
      padding: 0.25rem 1.25rem
      border: 2px solid black
      display: block
      &.inner_black
        background-color: black
        color: $c_white
      &.rotate_01
        transform: rotate(4deg)
      &.rotate_02
        transform: rotate(-3deg)
      &.rotate_03
        transform: rotate(-15deg)

// ====================
//      RWD
// ==============================

// --------------------
//      DESKTOP
// ------------------------------
@media screen and (min-width: 880px)
  .grid
    padding: 3rem 3rem 15rem 3rem
    display: grid
    align-items: center
    grid-row-gap: 2rem
    grid-template-columns: repeat(3, calc(100% / 3))
    .grid_item
      margin: 0
  .thumbnail_box
    margin: 4rem
    .article_title
      top: -4rem
      left: 0
      writing-mode: horizontal-tb
      .title_inner
        &:before
          +size(0, auto)
    .article_description
      top: auto
      right: 0
      bottom: -3rem

// --------------------
//      SMALL_DESKTOP
// ------------------------------
@media screen and (min-width: 880px) and (max-width: 1060px)
  .thumbnail_box
    .article_title
      .title_inner
        font-size: 0.9rem
    .article_description
      font-size: 0.6rem
      .description_inner
        padding: 0.25rem 0.5rem

// --------------------
//      LARGE_DESKTOP
// ------------------------------
@media screen and (min-width: 1280px)
  .grid
    grid-template-columns: repeat(4, 25%)
    .grid_item
      &:nth-child(4n-2)
        margin-top: -4rem
        margin-bottom: 4rem
      &:nth-child(4n)
        margin-top: -2.5rem
  .thumbnail_box
    margin: 4rem 3.5rem

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  .thumbnail_box
    margin: 0
    .thumbnail_img
      width: 250px
      filter: none
    .article_title
      top: -4rem
      .title_inner
        &[data-hover]
          -webkit-text-stroke: none
          text-stroke: none
          -webkit-text-fill-color: black
          text-fill-color: black
          color: black
        &:before
          height: 0
          content: ""
          -webkit-text-stroke: 0
          text-stroke: 0
          -webkit-text-fill-color: black
          text-fill-color: black
          color: black
          position: absolute
          top: 0
          left: 0
          white-space: nowrap
          overflow: hidden
          transition: all 0.3s
    .article_description
      top: auto
      bottom: -4rem
</style>
