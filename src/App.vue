<template>
  <div id="app"
    @mousedown="mousedownHandler"
    @mouseup="draging = false"
    @mousemove="mousemoveHandler"
  >
    <box 
      :boxX="boxX"
      :boxY="boxY"
      :boxZ="boxZ"
      :rotateX="rotateX"
      :rotateY="rotateY"
      :rotateZ="rotateZ"
      :translateY="translateY"
      :imgX="imgX"
      :imgY="imgY"
      :imgZ="imgZ"
    />
    <div class="setting">
      <p style="color: #999;">鼠标拖动页面旋转盒子角度</p>
      <div class="btn">rotateX: <input type="text" v-model="rotateX" /></div>
      <div class="btn">rotateY: <input type="text" v-model="rotateY" /></div>
      <div class="btn">rotateZ: <input type="text" v-model="rotateZ" /></div>
      <div class="btn">translateY: <input type="text" v-model="translateY" /></div>
      <div class="btn btn-scan" @click="addScan">{{ imgX ? '取消皮肤' : '添加皮肤' }}</div>
    </div>
  </div>
</template>

<script>
import box from './components/box.vue'

export default {
  name: 'App',
  components: {
    box
  },
  data () {
    return {
      boxX: 100,
      boxY: 100,
      boxZ: 100,
      imgX: '',
      imgY: '',
      imgZ: '',
      rotateX: -10,
      rotateY: -15,
      rotateZ: 0,
      translateY: 0,
      draging: false
    }
  },
  methods: {
    addScan () {
      if (!this.imgX) {
        this.imgX = '/img1.png'
        this.imgY = '/img2.png'
        this.imgZ = '/img2.png'
      } else {
        this.imgX = this.imgY = this.imgZ = ''
      }
    },
    mousedownHandler (e) {
      this.pageXstart = e.pageX
      this.pageYstart = e.pageY
      this.draging = true
    },
    mousemoveHandler (e) {
      if (this.draging) {
        this.rotateY = e.pageX - this.pageXstart
        this.rotateX = e.pageY - this.pageYstart
      }
    }
  }
}
</script>

<style scoped lang="scss">
.setting {
  text-align: center;
  margin-top: 30px;
  display: flex;
  flex-direction: column;
  .btn {
    display: block;
    margin-bottom: 10px;
  }
  .btn-scan {
    margin: 0 auto;
    width: 80px;
    padding: 5px 10px;
    border-radius: 4px;
    display: inline-block;
    background: #eee;
    cursor: pointer;
  }
}
/deep/ .box {
  &::before {
    text-align: right;
    content: 'Z';
    display: block;
    position: absolute;
    bottom: 0;
    top: 50%;
    width: 100%;
    height: 0;
    margin-top: -1px;
    border: 2px solid yellow;
    transform: rotateY(90deg);
  }
  .inner {
    &::before {
      text-align: right;
      content: 'X';
      display: block;
      position: absolute;
      bottom: 0;
      top: 50%;
      width: 100%;
      height: 0;
      margin-top: -1px;
      border: 2px solid red;
    }
    &::after {
      text-align: right;
      content: 'Y';
      display: block;
      position: absolute;
      left: 50%;
      top: 0;
      width: 0;
      height: 100%;
      margin-left: -1px;
      border: 2px solid blue;
    }
  }
}
</style>
