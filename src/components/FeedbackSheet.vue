<template lang="pug">
form#feedback_sheet(:action="feedbackUrl"
                    method="post")
  h2 聯絡姊弟
  .name_box
    input(name="name"
          placeholder="你的名字")
    span.input_focus
    label(for="name")
      i.far.fa-user
  .email_box
    input(name="email"
          placeholder="你的信箱")
    span.input_focus
    label(for="email")
      i.far.fa-envelope
  .topic_box
    select(name="option")
      option(value="0"
              disabled
              selected) 選擇主題
      option(value="1") 商業洽談
      option(value="2") 美食推薦
      option(value="3") 經驗分享
      option(value="4") 其他
    label(for="option")
      i.fas.fa-align-left
    label.icon_chevron(for="option")
      i.fas.fa-chevron-down
  .comment_box
    textarea(name="comment"
              placeholder="請輸入內容"
              rows="6")
    span.input_focus
    label(for="comment")
      i.far.fa-comment
  .recommendation_box
    label
      input(name="recommand"
            type="radio"
            value="yes")
      h4 喜歡這個網站
    label
      input(name="recommand"
            type="radio"
            value="no")
      h4 普普通通
  input(name="json"
        type="hidden"
        value="true")
  .response
  button.btn_ajax(@click.prevent="postFeedback()") 送出
</template>

<script>
export default {
  data () {
    return {
      feedbackUrl: 'https://2017.awiclass.monoame.com/api/demo/feedback'
    }
  },
  methods: {
    postFeedback () {
      let feedback = $('#feedback_sheet').serializeArray()
      feedback.find(obj => obj.name === 'json').value = 'true'
      $.ajax({
        url: this.feedbackUrl,
        method: 'post',
        data: feedback,
        success: function (result) {
          $('.response').text(result.response)
        }
      })
    }
  }
}
</script>

<style lang="sass">
@import "@/styles/global.sass"

// ====================
//      MAIN
// ==============================
#feedback_sheet
  padding: 3rem 0
  background-color: $c_black
  +center_flex
  flex-direction: column
  &>*
    margin: 0 0 1.5rem 0
  h2
    margin: 0 0 3rem 0
    font-size: 1.4rem
    color: white
  .input_focus
    +size(calc(100% + 2px), calc(100% + 2px), 3px)
    border: 2px solid $c_orange_01
    position: absolute
    top: -1px
    left: -1px
    transform: scale(1.1, 1.4)
    opacity: 0
    pointer-events: none
    transition: 0.4s
  .name_box, .email_box, .topic_box, .comment_box
    label
      +center_position
      left: 5%
      +center_flex
      i
        font-size: 1.2rem
        color: $c_orange_02
  .topic_box
    select
      cursor: pointer
      transition: 0.5s
      &:hover
        background-color: lighten($c_orange_01, 20)
        color: white
        transition: 0
    .icon_chevron
      right: 2.5%
      left: auto
      pointer-events: none
      i
        font-size: 1rem
  .comment_box
    .input_focus
      +size(calc(100% + 2px), calc(100% - 4px), 3px)
    label
      top: 10%
  input[name="name"], input[name="email"], select, textarea
    width: 50vw
    max-width: 500px
    min-width: 300px
    padding: 0.5rem 1rem 0.5rem 3rem
    border: 1px solid $c_orange_01
    border-radius: 3px
    background-color: white
    font-size: 1rem
    color: $c_black
    opacity: 0.9
    outline: none
    &::placeholder
      color: rgba($c_black, 0.3)
    &:focus
      +.input_focus
        transform: scale(1)
        opacity: 1
  select, input[name="recommand"]
    appearance: none
  .recommendation_box
    +center_flex
    label
      margin: 0
      +center_flex
      cursor: pointer
      &:nth-child(1)
        margin: 0 1.5rem 0 0
      input[name="recommand"]
        +size(1rem, 1rem, 50%)
        margin: 0 0.5rem 0 0
        border: 2px solid white
        cursor: pointer
        transition: 0.3s
        &:checked
          background-color: $c_orange_01
          outline: none
      h4
        margin: 0
        font-size: 1rem
        color: white
  .response
    margin: 0 0 1.5rem 0
    font-size: 1rem
    color: white
  .btn_ajax
    margin: 0
    padding: 5px 15px
    border: 2px solid white
    border-radius: 5px
    background-color: white
    font-size: 1rem
    font-weight: 700
    color: black
    cursor: pointer
    outline: none
    transition: 0.3s
    &:hover
      border: 2px solid $c_orange_02
      background-color: $c_orange_02
      color: white

// ====================
//      RWD
// ==============================

// --------------------
//      MOBILE
// ------------------------------
@media screen and (max-width: 880px)
  #feedback_sheet
    .name_box, .email_box, .topic_box, .comment_box
      label
        left: 8%
</style>
