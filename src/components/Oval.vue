<template>
  <div :class="{'oval': true, 'active': active}" :style="style" @mouseleave="mouseleave" @mouseup="mouseleave" @mousedown="mousedown">
      <div class="text">{{ text }}</div>
  </div>
</template>

<script>
export default {
  name: 'Oval',
  props: {
    bgColor: {
        type: String,
        default: '#FFF'
    },
    text: {
        type: String,
        default: ''
    }
  },
  data() {
      return {
          active: false
      }
  },
  computed: {
      style() {
          return {
              'backgroundColor': this.bgColor
          }
      }
  },
    methods: {
      mousedown() {
          this.active = true;
          this.$emit('click');
      },
      mouseleave() {
          this.active = false;
      }
  }
}
</script>

<style lang="less">
.oval {
    display: flex;
    justify-content: center;
    width: 58px;
    height: 46px;
    border-radius: 30px;
    box-shadow: inset 0px 0px 2px #fff, 0px 7px 0px 0px #555, 0px 10px 5px #fff;
    margin-right: 9px;
    font-weight: 900;
    color: rgb(181, 153, 152);
    transition: all 0.1s linear;
    .text {
        margin-top: 8px;
    }
    &.active {
        box-shadow: inset 0px 0px 2px #fff, 0px 2px 0px 0px #555, 0px 2px 3px #fff;;
        transform: translate(2px, 5px);
    }
}
</style>
