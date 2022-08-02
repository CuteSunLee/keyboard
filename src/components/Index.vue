<template>
  <div class="keyboard">
    <h1 v-if="showTitle">情人节快乐</h1>
    <div class="text" :style="{color: currentColor}">当前色值：{{ currentColor || '你猜' }}</div>
    <div class="hello">
    <div class="line line-one">
      <oval-item v-for="(item, index) in lineOne" :bg-color="colorlineOne[index]" :text="item"/>
    </div>
    <div class="line line-two">
      <circle-item :current-key="currentKey" v-for="(item, index) in lineTwo" :bg-color="colorlineTwo[index]" :text="item" @click="play(item, colorlineTwo[index])"/>
      <double-circle :bg-color="colorlineTwo[colorlineTwo.length - 1]" text="Del" />
    </div>
    <div class="line line-three">
      <circle-item :current-key="currentKey" v-for="(item, index) in lineThree" :bg-color="colorlineThree[index]" :text="item" @click="play(item, colorlineThree[index])"/>
    </div>
    <div class="line line-four">
      <double-circle :bg-color="colorlineFour[0]" text="caps" />
      <circle-item :current-key="currentKey" v-for="(item, index) in lineFour" :bg-color="colorlineFour[index + 1]" :text="item" @click="play(item, colorlineFour[index + 1])"/>
      <double-circle :bg-color="colorlineFour[colorlineFour.length - 1]" text="enter" />
    </div>
    <div class="line line-five">
      <double-circle :bg-color="colorlineFive[0]" text="shift" />
      <circle-item :current-key="currentKey" v-for="(item, index) in lineFive" :bg-color="colorlineFive[index + 1]" :text="item" @click="play(item, colorlineFive[index + 1])"/>
    </div>
    <div class="line line-six">
      <circle-item v-for="(item, index) in lineSixFront" :bg-color="colorlineSix[index]" :text="item" @click="play(item, colorlineSix[index])"/>
      <space-item :bg-color="colorlineSix[colorlineSix.length - 1]"/>
      <circle-item v-for="(item, index) in lineSixEnd" :bg-color="colorlineSixEnd[index]" :text="item" @click="play(item), colorlineSixEnd[index]"/>
    </div>
    <audio class="audio"
        v-for="item in letter"
        :src="audioSrc[item]"
        controls
        :id="item"
        hidden="true">
    </audio>
  </div>
  </div>
</template>

<script>
const LINE_ONE = ['esc', 'F1', 'F2', 'F', 'F4', 'F5', 'F6', 'F7', 'F8', 'F9', 'F10', 'F11', 'F12', 'Del']
const LINE_TWO = ['`~', '1!', '2@', '3#', '4$', '5%', '6^', '7&', '8*', '9(', '0)', '-_', '=+']
const LINE_THREE = ['tab', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '[{', ']}', '\\\|']
const LINE_FOUR = ['A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', ';:', '"']
const LINE_FIVE = ['Z', 'X', 'C', 'V', 'B', 'N', 'M', ',<', '.>', '/?', 'shift', '^']
const LINE_SIX_FRONT = ['fn', 'ctrl', 'alt', '⌘']
const LINE_SIX_END = ['⌘', 'alt', 'ctrl', '<', 'v', '>']
const LETTER = ['A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P']
const ALL = [...LINE_ONE, ...LINE_TWO, ...LINE_THREE, ...LINE_FOUR, ...LINE_FIVE, ...LINE_SIX_FRONT, ...LINE_SIX_END]

import Circle from './Circle.vue';
import Oval from './Oval.vue';
import DoubleCircle from './Double-circle.vue'
import Space from './Space.vue'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      currentKey: '123',
      audio: '',
      audioSrc: {
        A: require("@/assets/A.mp3"),
        S: require("@/assets/S.mp3"),
        D:require("@/assets/D.mp3"),
        F:require("@/assets/F.mp3"),
        G:require("@/assets/G.mp3"),
        H:require("@/assets/H.mp3"),
        J:require("@/assets/J.mp3"),
        K:require("@/assets/K.mp3"),
        L:require("@/assets/L.mp3"),
        Q:require("@/assets/Q.mp3"),
        W:require("@/assets/W.mp3"),
        E:require("@/assets/E.mp3"),
        R:require("@/assets/R.mp3"),
        T:require("@/assets/T.mp3"),
        Y:require("@/assets/Y.mp3"),
        U:require("@/assets/U.mp3"),
        I:require("@/assets/I.mp3"),
        O:require("@/assets/O.mp3"),
        P:require("@/assets/P.mp3"),
        Z:require("@/assets/Z.mp3"),
        X:require("@/assets/X.mp3"),
        C:require("@/assets/C.mp3"),
        V:require("@/assets/V.mp3"),
        B:require("@/assets/B.mp3"),
        N:require("@/assets/N.mp3"),
        M:require("@/assets/M.mp3"),
      },
      showTitle: false,
      inputList: [],
      letter: LETTER,
      currentSrc: '',
      currentColor: '',
      lineOne: LINE_ONE,
      lineTwo: LINE_TWO,
      lineThree: LINE_THREE,
      lineFour: LINE_FOUR,
      lineFive: LINE_FIVE,
      lineSixFront: LINE_SIX_FRONT,
      lineSixEnd: LINE_SIX_END,
      colorlineOne: ['rgb(203, 163, 140)', 'rgb(217, 146, 144)', 'rgb(163, 113, 87)', 'rgb(216, 142, 141)', 'rgb(209, 90, 96)', 'rgb(118, 51, 60)', 'rgb(178, 69, 74)', 'rgb(205, 100, 133)', 'rgb(126, 79, 99)', 'rgb(159, 104, 108)', 'rgb(214, 137, 145)', 'rgb(224, 12, 119)', 'rgb(214, 134, 145)', 'rgb(114, 55, 77)'],
      colorlineTwo: ['rgb(159, 134, 148)', 'rgb(84, 78, 85)', 'rgb(127, 90, 74)', 'rgb(175,	95,	94)', 'rgb(187, 85,	89)', 'rgb(132, 76, 81)', 'rgb(227, 112, 120)', 'rgb(110, 65, 70)', 'rgb(197, 169, 270)', 'rgb(81, 51, 56)', 'rgb(152, 153, 155)', 'rgb(217, 131, 142)', 'rgb(147 ,147 ,149)', 'rgb(212, 157, 197)'],
      colorlineThree: ['rgb(154, 129, 142)', 'rgb(159, 128, 162)', 'rgb(166, 95, 85)', 'rgb(216, 134, 158)', 'rgb(224, 125, 162)', 'rgb(142, 48, 78)', 'rgb(222, 181, 141)', 'rgb(208, 90, 126)', 'rgb(94, 43, 62)', 'rgb(150, 150, 152)', 'rgb(221, 106, 113)', 'rgb(166, 47, 53)', 'rgb(215, 102, 109)', 'rgb(77, 29, 45)'],
      colorlineFour: ['rgb(211, 189, 156)', 'rgb(222, 188, 177)', 'rgb(121, 76, 47)', 'rgb(201, 124, 132)', 'rgb(168, 46, 51)', 'rgb(104, 22, 34)', 'rgb(212, 64, 62)', 'rgb(111, 43, 68)', 'rgb(170, 94, 142)', 'rgb(137, 54, 81)', 'rgb(208, 153, 184)', 'rgb(161, 56, 77)', 'rgb(221, 87, 100)'],
      colorlineFive: ['rgb(221, 184, 173)', 'rgb(216, 169, 159)', 'rgb(219, 158, 156)', 'rgb(216, 147, 142)', 'rgb(203, 126, 135)', 'rgb(176, 63, 114)', 'rgb(208, 127, 134)', 'rgb(221, 90, 111)', 'rgb(223, 106, 114)', 'rgb(198, 83, 120)', 'rgb(111, 61, 82)', 'rgb(128, 34, 67)', 'rgb(166, 58, 79)'],
      colorlineSix: ['rgb(2018, 195, 151)', 'rgb(203, 195, 192)', 'rgb(202, 194, 191)', 'rgb(208, 159, 142)', 'rgb(96, 62, 44)'],
      colorlineSixEnd: ['rgb(190, 78, 128)', 'rgb(218, 180, 153)', 'rgb(212, 206, 174)', 'rgb(212, 156, 187)', 'rgb(163, 60 ,81)', 'rgb(164, 59, 79)']
    }
  },
  components: {
    'circle-item':Circle,
    'oval-item':Oval,
    'double-circle': DoubleCircle,
    'space-item': Space
  },
  methods: {
    play(type, color) {
      if (!LETTER.includes(type)) {
        return;
      }
      if (this.currentType) {
        this.currentColor = color;
        if (type !== this.currentType) {
          this.audio.pause();
        } else {
          return;
        }
      }
      this.currentType = type;
      this.audio = document.getElementById(type);
      this.audio.currentTime = 0;
      this.audio.play();
    },
  },
  mounted() {
    const _this = this;
    window.addEventListener('keydown', function(e) {
        _this.currentKey = e.key;
        _this.inputList.push(e.key);
        if (_this.inputList.join("").includes('qrjkl')) {
          _this.showTitle = true;
          _this.$emit('show');
        }
    });
    window.addEventListener('keyup', function(e) {
        _this.currentKey = '';
    });
  }
}
</script>

<style lang="less">
.keyboard {
  margin-top: 100px;
  h1 {
    position: absolute;
    left: 50%;
    top: 3%;
    transform: translate(-50%);
    color: #FFF;
  }
  .text {
    font-size: 20px;
    font-weight: 800;
    margin-bottom: 20px;
    text-align: center;
  }
  .hello {
    width: 1000px;
    background: rgb(64, 40, 33);
    padding: 20px;
    border-radius: 40px;
    box-shadow: inset 20px 20px 30px rgba(0, 0, 0, 0.3), inset -20px -20px 30px rgba(255, 255, 255, 0.2);
    .line {
      display: flex;
      margin-bottom: 12px;
    }
    .line-one, .line-three {
      margin-left: 30px;
    }
    .line-five {
      margin-left: 36px;
    }
    .line-three, .line-five {
      .circle {
        margin-right: 7px;
      }
    }
  }
}

</style>
