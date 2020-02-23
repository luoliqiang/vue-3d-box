<template>
  <div id="app"
    @mousedown="mousedownHandler"
    @mouseup="draging = false"
    @mousemove="mousemoveHandler"
  >
    <box 
      :boxX="100"
      :boxY="100"
      :boxZ="100"
      :rotateX="rotateX"
      :rotateY="rotateY"
      :rotateZ="rotateZ"
      :translateY="translateY"
    />
    <div class="setting">
      <div class="btn">rotateX: <input type="text" v-model="rotateX" /></div>
      <div class="btn">rotateY: <input type="text" v-model="rotateY" /></div>
      <div class="btn">rotateZ: <input type="text" v-model="rotateZ" /></div>
      <div class="btn">translateY: <input type="text" v-model="translateY" /></div>
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
      rotateX: -10,
      rotateY: -15,
      rotateZ: 0,
      translateY: 0,
      draging: false
    }
  },
  methods: {
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
