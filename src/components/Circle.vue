<template>
  <div :class="{'circle': true, 'active': active}" :style="style" @mouseleave="mouseleave" @mouseup="mouseleave" @mousedown="mousedown">
      <div class="text">{{ text }}</div>
  </div>
</template>

<script>

export default {
  name: 'Circle',
  props: {
    bgColor: {
        type: String,
        default: '#FFF'
    },
    text: {
        type: String,
        default: ''
    },
    currentKey: {
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
  watch: {
    currentKey(val) {
        this.active = val.toLowerCase() === this.text.toLowerCase();
    }
  },
  methods: {
      mousedown() {
        this.active = true;
        this.$emit('click');
      },
      mouseleave() {
          this.active = false;
      },
  },
}
</script>

<style lang="less">
.circle {
    display: flex;
    justify-content: center;
    width: 60px;
    height: 56px;
    border-radius: 60px;
    margin-right: 10px;
    font-weight: 900;
    color: rgb(181, 153, 152);
    box-shadow: inset 0px 0px 2px #fff, 0px 7px 0px 0px #555, 0px 9px 6px #fff;
    transition: all 0.1s linear;
    .text {
        margin-top: 8px;
    }
    &.active {
        box-shadow: inset 0px 0px 2px #fff, 0px 2px 0px 0px #555, 0px 2px 3px #fff;;
        transform: translate(3px, 5px);
    }
}
</style>
