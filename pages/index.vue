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
      radius: 70,
      curr: 0,
      start: 0,
      finish: 360,
      currentStep: 0
    }
  },
  methods: {
    animateCircleSegment2(draw_to = 0) {
      var canvas = document.getElementById('mainCircle');
      var ctx = canvas.getContext('2d');
      ctx.clearRect(0, 0, 150, 150);
      ctx.beginPath();
      ctx.strokeStyle = 'orange';
      ctx.arc(75, 75, 70, this.start, draw_to, false);
      ctx.stroke();
      this.curr = this.curr + 1;
      console.log(this.curr);
      if (this.curr < this.finish + 1) {
        requestAnimationFrame(() => {
          // Math.PI * 2 es la circunferencia 360ª
          this.animateCircleSegment2(Math.PI * 2 * this.curr / 100);
        });
      }
    },
    animateSegment(segmentName, width, height, from, to, current, clockwise) {
      let canvas = document.getElementById(segmentName);
      let radius = (width /2) - 10;
      let context = canvas.getContext('2d');
      context.clearRect(0, 0, width, height);
      context.beginPath();
      context.strokeStyle = 'red';
      context.arc(width / 2, width / 2, radius, from, to, clockwise);
      context.stroke();

      current = current + 1;
      console.log((circunference * current) / 100);
      if (current <= to + 1) {
        requestAnimationFrame(() => {
          //console.log((circunference * current) / 100);
          //this.animateSegment(segmentName, width, height, from, to, (circunference * current) / 100, clockwise);
        });
      }
    },
    createAllCircles() {
      this.createSegment('mainCircle', 0, 360, false);
      // this.createSegment('firstSegment', 0, 72, false);
      // this.createSegment('secondSegment', 72, 144, false);
      // this.createSegment('thirdSegment', 144, 288, false);
      // this.createSegment('fourthSegment', 288, 360, false);

      // this.createSegment('firstFinalSegment', 288, 72, false);
      // this.createSegment('secondFinalSegment', 288, 72, true);
    },
    createSegment(canvasName, from, to, clockwise) {
      const canvas = document.getElementById(canvasName);
      const context = canvas.getContext('2d');
      let centerX = canvas.width / 2;
      let centerY = canvas.height / 2;
      const radius = 70; //chequear esto

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
    // const container = document.getElementById('circle-container');
    // console.log('height', container.clientHeight);
    // console.log('width', container.offsetWidth);
    this.createAllCircles();
    this.animateCircleSegment2();
    //this.animateSegment('mainCircle', '150px', '150px', 0, 360, 0, false);
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
