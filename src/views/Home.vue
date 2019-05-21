<template lang="pug">
.home_page
  Header
  Logo
  Navbar
  Menu
  .article_list
    ClassificationBox
    Grid
    FeedbackSheet
</template>

<script>
import Header from '@/components/Header'
import Logo from '@/components/Logo'
import Navbar from '@/components/Navbar'
import Menu from '@/components/Menu'
import ClassificationBox from '@/components/ClassificationBox'
import Grid from '@/components/Grid'
import FeedbackSheet from '@/components/FeedbackSheet'

export default {
  components: {
    Header, Logo, Navbar, Menu, ClassificationBox, Grid, FeedbackSheet
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================

// ====================
//      RWD
// ==============================

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  .article_list
    height: auto
    min-height: 0
    display: flex
    flex-direction: column
</style>
