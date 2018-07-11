<!--<div style="width: 400px;height: 400px">-->
<!--<progress-ring :percent="0.8" :radius="50"></progress-ring>-->
<!--</div>-->
<template>
  <div class="pro-wrapper" ref="id">
    <svg width="100%" height="100%"  class="center">
      <defs>
        <linearGradient x1="1" y1="0" x2="0" y2="0" :id=lgId1>
          <stop offset="0%" :stop-color="getColor(0)"></stop>
          <stop offset="100%" :stop-color="getColor(1)"></stop>
        </linearGradient>
        <linearGradient x1="1" y1="0" x2="0" y2="0" :id=lgId2>
          <stop offset="0%" :stop-color="getColor(1)"></stop>
          <stop offset="100%" :stop-color="getColor(2)"></stop>
        </linearGradient>
      </defs>
      <g >
        <circle cx="50%" cy="50%" :r=radius stroke-width="20"
                stroke="#08465B" fill="none" ></circle>
        <circle cx="50%" cy="50%" :r=radius stroke-width="15" stroke-linecap="round"
                :stroke= getLgId(lgId1) fill="none" stroke-dasharray=" 0 0" ></circle>
        <circle class="nextCircle"
                cx="50%" cy="50%" :r=radius stroke-width="15"
                stroke-dasharray="0 0" stroke-linecap="round"
                :stroke= getLgId(lgId2) fill="none"></circle>
      </g>
    </svg>
    <div class="pro-wrapper-text">{{formatter(percent)}}</div>
  </div>
</template>

<script>
export default {
  name: 'progressRing',
  props: {
    radius: {
      type: Number,
      default: 80
    },
    colors: {
      type: Array,
      default: () => ['#2ED698', '#2BD2C7', '#29CEF2']
    },
    percent: {
      type: Number,
      default: 0
    },
    formatter: {
      type: Function,
      default: val => val
    },
    id: {
      type: String,
      default: () => (Math.floor(1000000 * Math.random())).toString().padStart(6, '0')
    },
    lgId1: {
      type: String,
      default: () => (Math.floor(1000000 * Math.random())).toString().padStart(6, '0')
    },
    lgId2: {
      type: String,
      default: () => (Math.floor(1000000 * Math.random())).toString().padStart(6, '0')
    }
  },
  data() {
    return {
    };
  },
  mounted() {
    this.renderCircle();
  },
  watch: {
    percent(curVal, oldVal) {
      if (curVal !== oldVal) {
        this.renderCircle();
      }
    }
  },
  methods: {
    renderCircle() {
      const cirleElem = this.$refs.id.querySelector('.nextCircle');
      if (cirleElem) {
        const bbox = cirleElem.getBBox();
        cirleElem.setAttribute('transform', `rotate(180 ${bbox.x + (bbox.width / 2)} ${bbox.y + (bbox.height / 2)})`);
      }
      const eleCircles = this.$refs.id.querySelectorAll('circle');
      const halfCircleLen = this.radius * Math.PI;
      const circleLen = halfCircleLen * 2;
      const percent = this.percent;
      const proLen = percent * circleLen;
      if (percent < 0.5) {
        eleCircles[1].setAttribute('stroke-dasharray', `${proLen} ${circleLen}`);
        // eleCircles[2].setAttribute('stroke-dasharray', `0 ${circleLen}`);
      } else {
        eleCircles[1].setAttribute('stroke-dasharray', `${halfCircleLen} ${circleLen}`);
        eleCircles[2].setAttribute('stroke-dasharray', `${proLen - halfCircleLen} ${circleLen}`);
      }
    },
    getColor(index = 0) {
      const colors = this.colors;
      return colors[index % (colors.length)];
    },
    getLgId(id) {
      return `url('#${id}')`;
    }
  }
};
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  .pro-wrapper{
    position: relative;
    width: 100%;
    height: 100%;
    transition: all 1s ease-out;
    &:hover{
      transform: scale(1.2);
      -webkit-transform: scale(1.2);
    }
    &-text{
      position: absolute;
      top: 50%;
      left: 0;
      width: 100%;
      text-align: center;
      margin: 0;
      transform: translateY(-50%);
      color: #B9DFFF;
      font-size: 18px;
    }
  }
</style>
