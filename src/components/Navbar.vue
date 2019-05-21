<template lang="pug">
.navbar
  NavItems
</template>

<script>
import NavItems from '@/components/NavItems'

export default {
  components: {
    NavItems
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.navbar
  width: 100%
  padding: 3vw 10vw
  position: fixed
  top: 0
  z-index: 1

// ====================
//      RWD
// ==============================

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  .navbar
    display: none
</style>
