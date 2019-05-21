<template lang="pug">
.classification_box
  .row
    .col-sm-12.title_box
      h4.title_eng ALL ARTICLES
      h2.title_ch 全部文章
      .lower_line
</template>

<script>
export default {

}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.classification_box
  +size(100%)
  margin: 5rem 0 2.5rem 0
  +center_flex
  flex-direction: column
  .row
    +size(80%, 100%)
    +center_flex
    .title_box
      +size(100%)
      max-width: 900px
      padding: 0
      +center_flex(center, flex-start)
      flex-direction: column
      .title_eng
        margin: 0 0 0.2rem 3.2rem
        font-size: 0.7rem
        font-weight: 400
        color: rgba($c_black, 0.5)
      .title_ch
        margin: 0 0 0.4rem 3rem
        font-size: 1.4rem
        color: $c_black
      .lower_line
        +size(90%, 1px)
        background-color: rgba($c_black, 0.2)
        +center_position
        top: 100%

// ====================
//      RWD
// ==============================

// --------------------
//      LARGE_DESKTOP
// ------------------------------
@media screen and (min-width: 1280px)
  .classification_box
    margin: 5rem 0
    .row
      .title_box
        max-width: 1200px
        .lower_line
          +size(95%, 1px)

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  .classification_box
      margin: 2.5rem 0 7.5rem 0
      .row
        .title_box
          .lower_line
            +size(85%, 1px)
</style>
