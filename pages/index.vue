<template>
  <div>
    <div id="circle-container">
      <canvas id="mainCircle" width="150" height="150"/>
      <canvas id="firstSegment" width="150" height="150"/>
      <canvas id="secondSegment" width="150" height="150"/>
      <canvas id="thirdSegment" width="150" height="150"/>
      <canvas id="fourthSegment" width="150" height="150"/>
    </div>
  </div>
</template>

<script>
const PI = Math.PI;
const circunference = PI * 2;

export default {
  data() {
    return {
      currentStep: 0
    }
  },
  methods: {
    animateCircleSegment(segmentName, color, width, height, start, finish, draw_to) {
      const canvas = document.getElementById(segmentName);
      let centerX = width / 2;
      let centerY = height / 2;
      let radius = (width / 2) - 5;
      const ctx = canvas.getContext('2d');
      ctx.clearRect(0, 0, width, height);
      ctx.beginPath();
      ctx.strokeStyle = color;
      ctx.lineWidth = 5;
      draw_to = !draw_to ? start : draw_to;
      ctx.arc(centerX, centerY, radius, start, draw_to, false);
      ctx.stroke();

      if (draw_to < finish) {
        requestAnimationFrame(() => {
          this.animateCircleSegment(segmentName, color, width, height, start, finish, draw_to + this.getRadians(2));
        });
      }
    },
    createAllCircles() {
      this.createSegment('mainCircle', 150, 150, 0, 360, false);
      //this.createSegment('firstSegment', 0, 72, false);
      // this.createSegment('secondSegment', 72, 144, false);
      // this.createSegment('thirdSegment', 144, 288, false);
      // this.createSegment('fourthSegment', 288, 360, false);

      // this.createSegment('firstFinalSegment', 288, 72, false);
      // this.createSegment('secondFinalSegment', 288, 72, true);
    },
    createSegment(canvasName, width, height, from, to, clockwise) {
      const canvas = document.getElementById(canvasName);
      const context = canvas.getContext('2d');
      let centerX = width / 2;
      let centerY = height / 2;
      let radius = (width / 2) - 5;

      context.beginPath();
      context.arc(centerX, centerY, radius, this.getRadians(from), this.getRadians(to), clockwise);
      context.fillStyle = 'transparent';
      context.fill();
      context.lineWidth = 5;
      context.strokeStyle = 'gray';
      context.stroke();
    },
    getRadians(degrees) {
      return(degrees * (PI / 180));
    }
  },
  mounted() {
    this.createAllCircles();
    this.animateCircleSegment('mainCircle', 'grey', 150, 150, this.getRadians(0), this.getRadians(360));
    // setTimeout(() =>{ this.animateCircleSegment3('secondSegment', 'gray', 150, 150, this.getRadians(0), this.getRadians(72)) }, 5000);
  }
}
</script>

<style>
  #circle-container {
    position: relative;
    width: 150px;
    height: 150px;
  }

  canvas  {
    border: 1px solid;
    position: absolute;
    transform: rotate(-90deg);
  }
</style>
