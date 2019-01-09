<template>
  <canvas id="sketch" ref="cv"
    @mousedown="startDrawing"
    @mousemove="drawing"
    @mouseup="endDrawing"></canvas>  
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  data () {
    return {
      cv: null as any as HTMLCanvasElement,
      ctx: null as any as CanvasRenderingContext2D,
      isDrawing: false,
    }
  },

  mounted () {
    const cv = this.$refs.cv as HTMLCanvasElement;
    this.cv = cv;
    cv.height = window.innerHeight;
    cv.width = window.innerWidth;
    const ctx = cv.getContext('2d') as CanvasRenderingContext2D;
    this.ctx = ctx;

    // this.loadImg('http://wx4.sinaimg.cn/large/d8eedf34gy1fxelf4x3fkj212w0px4qq.jpg');
    this.drawMask();

    cv.addEventListener('touchstart', (ev) => {
      ev.preventDefault();
      const {clientX, clientY} = ev.touches[0];
      const mockEV = {x: clientX, y: clientY} as any;
      this.startDrawing(mockEV);
    });
    cv.addEventListener('touchmove', (ev) => {
      ev.preventDefault();
      const {clientX, clientY} = ev.touches[0];
      const mockEV = {x: clientX, y: clientY} as any;
      this.drawing(mockEV);
    });
    cv.addEventListener('touchEnd', (ev: any) => {
      ev.preventDefault();
      const {clientX, clientY} = ev.touches[0];
      const mockEV = {x: clientX, y: clientY} as any;
      this.endDrawing(mockEV);
    });
  },

  methods: {
    loadImg (imgUrl: string) {
      const img = new Image();
      img.src = imgUrl;
      img.onload = () => {
        this.ctx.drawImage(img, 0, 0);
        this.drawMask();
      }
    },
    drawMask () {
      const {cv, ctx} = this;
      ctx.fillStyle = 'white';
      ctx.fillRect(0, 0, cv.width, cv.height);
      ctx.globalCompositeOperation="destination-out";
    },
    startDrawing(ev: MouseEvent) {
      this.isDrawing = true;
      const {ctx} = this;
      const {x, y} = ev;

      ctx.globalCompositeOperation="destination-out";
      ctx.strokeStyle = 'rgba(0,0,0,0.1)';
      ctx.lineCap = 'round';
      ctx.lineJoin="round";
      // ctx.strokeStyle = 'red';
      ctx.lineWidth = 30;

      ctx.beginPath();
      ctx.moveTo(x, y);
    },
    drawing(ev: MouseEvent) {
      if (!this.isDrawing) { return; }
      const {x, y} = ev;
      const {ctx} = this;
      ctx.lineTo(x, y);
      ctx.stroke();
      ctx.closePath();

      ctx.beginPath();
      ctx.moveTo(x, y);
    },
    endDrawing(ev: MouseEvent) {
      this.isDrawing = false;
      const {x, y} = ev;
      const {ctx} = this;
      ctx.lineTo(x, y);
      ctx.stroke();
      ctx.closePath();
    }
  }
});
</script>

<style lang="scss" scoped>

</style>
