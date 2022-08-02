<template>
  <div :class="{'double-circle': true, 'active': active}" :style="style" @mouseleave="mouseleave" @mouseup="mouseleave" @mousedown="mousedown">
      <div class="text">{{ text }}</div>
  </div>
</template>

<script>
export default {
  name: 'DoubleCircle',
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
.double-circle {
    position: relative;
    display: flex;
    justify-content: center;
    width: 126px;
    height: 60px;
    border-radius: 60px;
    margin-right: 8px;
    font-weight: 900;
    color: rgb(181, 153, 152);
    overflow: hidden;
    transition: all 0.1s linear;
    box-shadow: inset 0px 0px 2px #fff, 0px 7px 0px 0px #555, 0px 10px 5px #fff;
    &::before, &::after {
        content: "";
        width: 80px;
        height: 70px;
        border-radius: 60px;
        background:rgb(63, 42, 33);
        position: relative;
    }
    &::before {
        position: absolute;
        top: -60px;
    }
    &::after {
        position: absolute;
        bottom: -60px;
    }
    .text {
        margin-top: 8px;
    }
    &.active {
        box-shadow: inset 0px 0px 2px #fff, 0px 2px 0px 0px #555, 0px 2px 3px #fff;;
        transform: translate(2px, 5px);
    }
}
</style>
