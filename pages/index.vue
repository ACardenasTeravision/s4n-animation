<template>
  <div>
    <div id="circle-container">
      <canvas id="mainCircle" width="150" height="150"/>
      <canvas id="firstSegment" width="150" height="150"/>
      <!-- <canvas id="secondSegment" width="150" height="150"/>
      <canvas id="thirdSegment" width="150" height="150"/>
      <canvas id="fourthSegment" width="150" height="150"/> -->
    </div>
    <h1>{{ currentStep }}</h1>
    <button @click="this.increment">+</button>
    <button @click="this.decrement">-</button>
  </div>
</template>

<script>
const PI = Math.PI;
const circunference = PI * 2;

export default {
  data() {
    return {
      currentStep: 0,
      moveForward: true
    }
  },
  methods: {
    increment() {
      this.currentStep = this.currentStep + 1;
      this.moveForward = true;
    },
    decrement() {
      this.currentStep = this.currentStep - 1;
      this.moveForward = false;
    },
    animateCircleSegment(segmentName, color, width, height, start, finish, anticlockwise, draw_to) {
      const canvas = document.getElementById(segmentName);
      let centerX = width / 2;
      let centerY = height / 2;
      let radius = (width / 2) - 5;
      const ctx = canvas.getContext('2d');
      //ctx.clearRect(0, 0, width, height);
      ctx.beginPath();
      ctx.strokeStyle = color;
      ctx.lineWidth = 5;
      draw_to = !draw_to ? start : draw_to;
      ctx.arc(centerX, centerY, radius, start, draw_to, anticlockwise);
      ctx.stroke();
      ctx.closePath();
      if (draw_to < finish) {
        requestAnimationFrame(() => {
          anticlockwise ?
            this.animateCircleSegment(segmentName, color, width, height, start, finish, anticlockwise, draw_to - this.getRadians(2)):
            this.animateCircleSegment(segmentName, color, width, height, start, finish, anticlockwise, draw_to + this.getRadians(2))
        });
      }
    },
    createAllCircles() {
      this.createSegment('mainCircle', 150, 150, 0, 360, false);
    },
    createSegment(canvasName, width, height, from, to, anticlockwise) {
      const canvas = document.getElementById(canvasName);
      const context = canvas.getContext('2d');
      let centerX = width / 2;
      let centerY = height / 2;
      let radius = (width / 2) - 5;

      context.beginPath();
      context.arc(centerX, centerY, radius, this.getRadians(from), this.getRadians(to), anticlockwise);
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
    //this.animateCircleSegment('mainCircle', 'red', 150, 150, this.getRadians(144), this.getRadians(288));
    // setTimeout(() =>{ this.animateCircleSegment3('secondSegment', 'gray', 150, 150, this.getRadians(0), this.getRadians(72)) }, 5000);
  },
  watch: {
    currentStep: function (val) {
      if(val < 0) {
        this.currentStep = 0;
      } else if (val > 7) {
        this.currentStep = 8;
      } else {
        switch (val) {
          case 0:
            if(this.moveForward == false) {
              console.log('ANIMANDO HACIA EL PASO 0');
              this.animateCircleSegment('firstSegment', 'orange', 150, 150, this.getRadians(72), this.getRadians(0), true);
            }
          break;
          case 1:
            console.log('STEP', this.currentStep);
            console.log('DIRECCION', this.moveForward);
            console.log('ANIMANDO HACIA EL PASO 1');
            this.animateCircleSegment('firstSegment', 'red', 150, 150, this.getRadians(0), this.getRadians(72), false);
          break;
          case 2:
            console.log('STEP', this.currentStep);
            console.log('DIRECCION', this.moveForward);
            console.log('ANIMANDO HACIA EL PASO 2');
            this.animateCircleSegment('firstSegment', 'gray', 150, 150, this.getRadians(0), this.getRadians(72), false);
          break;
          case 3:
            console.log('STEP', this.currentStep);
            console.log('DIRECCION', this.moveForward);
            console.log('ANIMANDO HACIA EL PASO 3');
            this.animateCircleSegment('firstSegment', 'red', 150, 150, this.getRadians(72), this.getRadians(144), false);

          break;
          case 4:
            console.log('STEP', this.currentStep);
            console.log('DIRECCION', this.moveForward);
            console.log('ANIMANDO HACIA EL PASO 4');
            this.animateCircleSegment('firstSegment', 'gray', 150, 150, this.getRadians(72), this.getRadians(144), false);
          break;
          case 5:
            console.log('STEP', this.currentStep);
            console.log('DIRECCION', this.moveForward);
            console.log('ANIMANDO HACIA EL PASO 5');
            this.animateCircleSegment('firstSegment', 'red', 150, 150, this.getRadians(144), this.getRadians(288), false);
          break;
          case 6:
            console.log('STEP', this.currentStep);
            console.log('DIRECCION', this.moveForward);
            console.log('ANIMANDO HACIA EL PASO 6');
            this.animateCircleSegment('firstSegment', 'gray', 150, 150, this.getRadians(144), this.getRadians(288), false);
          break;
          case 7:
            console.log('STEP', this.currentStep);
            console.log('DIRECCION', this.moveForward);
            console.log('ANIMANDO HACIA EL PASO 7');
            this.animateCircleSegment('firstSegment', 'red', 150, 150, this.getRadians(288), this.getRadians(360), false);
          break;
        }
      }
    }
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
    position: absolute;
    transform: rotate(-90deg);
  }
</style>
