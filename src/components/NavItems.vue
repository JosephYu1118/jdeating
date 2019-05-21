<template lang="pug">
ul.navbar-nav
  li.nav-item.btn_articles(@click="moveToAnchor(1)")
    .nav_text 全部文章
    .nav_mask
      span 全部文章
  li.nav-item.btn_contact(@click="moveToAnchor(2)")
    .nav_text 聯絡姊弟
    .nav_mask
      span 聯絡姊弟
</template>

<script>
export default {
  methods: {
    moveToAnchor (anchor) {
      let offsetArticles = $('.article_list').offset().top
      let offsetContact = $('#feedback_sheet').offset().top
      if (anchor === 1) {
        if ($(window).width() > 880) {
          $('html, body').animate({
            scrollTop: offsetArticles - 40
          }, 700)
        } else if ($(window).width() <= 880) {
          $('html, body').animate({
            scrollTop: offsetArticles
          }, 700)
        }
      } else if (anchor === 2) {
        $('html, body').animate({
          scrollTop: offsetContact
        }, 700)
      }
    }
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.navbar-nav
  width: 50vw
  +center_position
  +center_flex(space-evenly)
  flex-direction: row
  .nav-item
    width: 6rem
    font-size: 1rem
    font-weight: 500
    color: white
    transform: translate(10px, 0)
    display: inline-block
    cursor: pointer
    transition: all 0.8s cubic-bezier(0.23, 1, 0.32, 1)
    &:before
      +size(4px, 120%)
      padding: 0
      content: ""
      background-color: $c_orange_01
      position: absolute
      top: -10%
      left: -20%
      z-index: -1
      transition: all 0.8s cubic-bezier(0.23, 1, 0.32, 1)
    &:hover
      text-decoration: none
      font-weight: 700
      color: white
      &:before
        background-color: $c_orange_02
        transform: translateX(1300%) scale(24, 0.2)
      .nav_text
        animation: fadingIn 0.8s forwards
      .nav_mask
        display: block
        animation: glitching 0.2s both
    .nav_mask
      +size(100%, 20%)
      position: absolute
      top: 20%
      display: none
      overflow: hidden
      backface-visibility: hidden
      span
        width: 100%
        position: absolute
        top: -100%
        left: 50%
        transform: translateX(-50%)
</style>
