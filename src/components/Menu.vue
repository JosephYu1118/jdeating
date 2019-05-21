<template lang="pug">
.menu
  NavItems
  .hamburger_box(@click="squashHamburger()")
    .hamburger
</template>

<script>
import NavItems from '@/components/NavItems'

export default {
  components: {
    NavItems
  },
  methods: {
    squashHamburger () {
      $('.hamburger').toggleClass('cross')
      $('.menu').toggleClass('menu_open')
    }
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.menu
  +size(5rem)
  background: transparent
  position: fixed
  top: 0
  right: 0
  opacity: 0
  transition: 0.5s
  &.menu_black
    .hamburger_box
      .hamburger
        background-color: rgba($c_black, 0.8)
        transition: background-color 0.4s
        &.cross
          background-color: rgba($c_black, 0)
          transition: background-color 0s
        &:before, &:after
          background-color: rgba($c_black, 0.8)
  &.menu_show
    z-index: 2
    opacity: 1
    transition: 0.4s
    .hamburger_box
      .hamburger
        opacity: 1
        transition: opacity 0.4s
  &.menu_open
    +size(30%)
    background: white
    .navbar-nav
      display: flex
    .hamburger_box
      .hamburger
        background-color: rgba($c_black, 0.8)
        &.cross
          background-color: rgba($c_black, 0)
        &:before, &:after
          background-color: rgba($c_black, 0.8)
  .navbar-nav
    width: 100%
    display: none
    flex-direction: column
    .nav-item
      margin: 1rem 0
      font-size: 1.2rem
      color: $c_black
      &:hover
        color: $c_black
        &:before
          transform: translateX(1400%) scale(30, 0.2)
  .hamburger_box
    +size(5rem)
    position: absolute
    top: 0
    right: 0
    cursor: pointer
    .hamburger
      +size(30px, 3px)
      background-color: white
      +center_position
      opacity: 0
      transition: background-color 0.4s
      &:before, &:after
        +size(30px, 3px)
        content: ""
        background-color: white
        position: absolute
        transition: all 0.4s, top 0.3s 0.3s cubic-bezier(0.23, 1, 0.32, 1), transform 0.3s cubic-bezier(0.23, 1, 0.32, 1)
      &:before
        top: -10px
      &:after
        top: 10px
      &.cross
        background-color: rgba(white, 0)
        transition: background-color 0s
        &:before, &:after
          top: 0
          left: -50%
          transition: all 0.4s, top 0.3s cubic-bezier(0.23, 1, 0.32, 1), transform 0.3s 0.3s cubic-bezier(0.23, 1, 0.32, 1)
        &:before
          transform: rotate(45deg)
        &:after
          transform: rotate(-45deg)

// ====================
//      RWD
// ==============================

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  .menu
    z-index: 2
    opacity: 1
    &.menu_open
      +size(100%, 15%)
      .nav-item
        margin: 0.5rem 0
        font-size: 1rem
        &:hover
          &:before
            transform: translateX(1300%) scale(24, 0.2)
    .hamburger_box
      .hamburger
        opacity: 1
</style>
