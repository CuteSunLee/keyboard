<template>
  <div :class="{'space': true, 'active': active}" :style="style" @mouseleave="mouseleave" @mouseup="mouseleave" @mousedown="mousedown">
      <div class="text">{{ text }}</div>
  </div>
</template>

<script>
export default {
  name: 'Space',
  props: {
    bgColor: {
        type: String,
        default: 'rgb(63, 42, 33)'
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
.space {
    display: flex;
    justify-content: center;
    width: 300px;
    height: 56px;
    border-radius: 60px;
    margin-right: 10px;
    font-weight: 900;
    color: rgb(181, 153, 152);
    transition: all 0.1s linear;
    box-shadow: inset 0px 0px 2px #fff, 0px 7px 0px 0px #555, 0px 10px 5px #fff;
    .text {
        margin-top: 8px;
    }
    &.active {
        box-shadow: inset 0px 0px 2px #fff, 0px 2px 0px 0px #555, 0px 2px 3px #fff;;
        transform: translate(2px, 5px);
    }
}
</style>
