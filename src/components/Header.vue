<template lang="pug">
.header
  h3 人文食記
  h1 挑食姊與嗜吃弟
  .mouse
    p Scroll
</template>

<script>
export default {
  data () {
    return {
      timer: null,
      counter: 0,
      position: ['15%', '80%', 'center']
    }
  },
  methods: {
    getCoverPosition () {
      if ($(window).width() <= 500) {
        $('.header').css({
          'background-position': this.position[0]
        })
        this.timer = window.setInterval(() => {
          this.counter++
          $('.header').animate({
            'background-position': this.position[this.counter % 2]
          }, {
            duration: 500,
            easing: 'linear'
          })
        }, 5000)
      } else if ($(window).width() > 500) {
        $('.header').css({
          'background-position': this.position[2]
        })
      }
    }
  },
  mounted () {
    this.getCoverPosition()
    $(window).resize(() => {
      clearInterval(this.timer)
      this.counter = 0
      this.getCoverPosition()
    })
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
.header
  height: 100vh
  background-image: url(../assets/jdeating_cover.jpg)
  background-size: auto 100vh
  background-position: center
  background-repeat: no-repeat
  +center_flex
  flex-direction: column
  h3
    font-size: 1.2rem
    color: rgba($c_white, 0.7)
  h1
    margin: 0.5rem 0
    font-size: 2.25rem
    color: $c_white
  .mouse
    +size($widthMouse, $heightMouse, 100px)
    background: $colorOutlineFade linear-gradient(transparent 0%, transparent 50%, $colorOutline 50%, $colorOutline 100%)
    background-size: 100% 200%
    position: absolute
    right: 5vw
    bottom: 5vh
    +center_flex
    animation: colorSlide $animDuration linear infinite, nudgeMouse $animDuration ease-out infinite
    &:before, &:after
      margin: auto
      content: ""
      position: absolute
      top: 0
      right: 0
      bottom: 0
      left: 0
    &:before
      +size($widthMouse - $borderMouse, $heightMouse - $borderMouse, 100px)
      background-color: $colorBg
    &:after
      +size($sizeTrackball, $sizeTrackball, 100%)
      background-color: $colorOutline
      animation: trackBallSlide $animDuration linear infinite
    p
      margin: 75px 0 0 0
      color: $colorOutline
      animation: colorText $animDuration ease-out infinite, nudgeText $animDuration ease-out infinite
</style>
