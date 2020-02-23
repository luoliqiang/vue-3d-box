<template>
  <div
    class="box"
    :style="{
      '--boxsize': boxsize + 'px',
      '--x': boxX + 'px',
      '--_x': '-' + boxX + 'px',
      '--y': boxY + 'px',
      '--_y': '-' + boxY + 'px',
      '--z': boxZ + 'px',
      '--_z': '-' + boxZ + 'px',
      '--rotatex': rotateX + 'deg',
      '--rotatey': rotateY + 'deg',
      '--rotatez': rotateZ + 'deg',
      '--translatey': translateY + 'px'
      }"
    >
    <div class="inner">
      <div class="item top" :style="{backgroundImage: 'url(' + imgY +')'}">
        <div class="open"></div>
      </div>
      <div class="item bottom" :style="{backgroundImage: 'url(' + imgY +')'}"></div>
      <div class="item front" :style="{backgroundImage: 'url(' + imgY +')'}"></div>
      <div class="item back" :style="{backgroundImage: 'url(' + imgY +')'}"></div>
      <div class="item right" :style="{backgroundImage: 'url(' + imgY +')'}"></div>
      <div class="item left" :style="{backgroundImage: 'url(' + imgY +')'}"></div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  props: {
    data: {
      default: ''
    },
    boxsize: {
      type: Number,
      default: 300
    },
    boxX: {
      type: Number,
      default: 100
    },
    boxY: {
      type: Number,
      default: 120
    },
    boxZ: {
      type: Number,
      default: 100
    },
    rotateX: {
      default: 100
    },
    rotateY: {
      default: 100
    },
    rotateZ: {
      default: 100
    },
    translateY: {
      default: 0
    },
    imgX: {type: String},
    imgY: {type: String},
    imgZ: {type: String}
  },
  data () {
    return {
    }
  },
  watch: {
    rotateX (val) {
      console.log(val)
    }
  }
}
</script>
<style scoped lang="scss">
.box {
  width: var(--boxsize);
  height: var(--boxsize);
  margin: 0 auto;
  border: 1px solid #000;
  -webkit-perspective: 8000px;
  perspective: 8000px;
  perspective-origin: 50% 50%;
  -webkit-perspective-origin: 50% 50%;
  -webkit-transform-style: preserve-3d;
  transform-style: preserve-3d;
  .inner {
    position: relative;
    width: 100%;
    height: 100%;
    -webkit-perspective: 8000px;
    perspective: 8000px;
    perspective-origin: 50% 0%;
    -webkit-perspective-origin: 50% 50%;
    -webkit-transform-style: preserve-3d;
    transform-style: preserve-3d;
    transform: rotateY(var(--rotatey)) rotateX(var(--rotatex)) rotateZ(var(--rotatez)) translateY(var(--translatey));
    // border: 2px solid yellow;
    // transform: rotateX(-15deg) rotateY(-10deg);
    // background: rgba(0,0,0,.2);
  }
  .item {
    position: absolute;
    background-size: cover;
    background-color :gray;
    background-position: center center;
  }
  .top {
    width: var(--x);
    height: var(--z);
    top: calc(50% - var(--z) / 2);
    left: calc(50% - var(--x) / 2);
    background-color :green;
    transform: translateY(calc(var(--_y) / 2)) rotateX(90deg);
    .open {
      opacity: 0;
      width: 100%;
      height: 100%;
      background: #000;
    }
  }
  .bottom {
    width: var(--x);
    height: var(--z);
    top: calc(50% - var(--z) / 2);
    left: calc(50% - var(--x) / 2);
    transform: translateY(calc(var(--y) / 2)) rotateX(90deg);
    background-color :green;
  }
  .right {
    position: relative;
    height: var(--y);
    width: var(--z);
    top: calc(50% - var(--y) / 2);
    left: calc(50% - var(--z) / 2);
    transform: translateX(calc(var(--x) / 2)) rotateY(90deg);
    background-color :red;
    &::before {
      content: '';
      position: absolute;
      left: 0;
      top: 0;
      height: 100%;
      // width: 200%;
      width: 100%;
      background: rgba(0,0,0,.4);
      border-radius: 0 0 0 5px;
    }
  }
  .left {
    height: var(--y);
    width: var(--z);
    top: calc(50% - var(--y) / 2);
    left: calc(50% - var(--z) / 2);
    transform: translateX(calc(var(--_x) / 2)) rotateY(90deg);
    background-color :red;
  }
  .front {
    height: var(--y);
    width: var(--x);
    top: calc(50% - var(--y) / 2);
    left: calc(50% - var(--x) / 2);
    transform: translateZ(calc(var(--z) / 2));
    background-color :purple;
  }
  .back {
    height: var(--y);
    width: var(--x);
    top: calc(50% - var(--y) / 2);
    left: calc(50% - var(--x) / 2);
    transform: translateZ(calc(var(--_z) / 2));
    background-color :purple;
  }
}
</style>
