<template>
  <div>
    <div class="circle-container">
      <canvas id="mainCircle" width="300" height="200"></canvas>
      <canvas id="myCanvas2" width="300" height="200"></canvas>
      <canvas id="myCanvas3" width="300" height="200"></canvas>
      <canvas id="myCanvas4" width="300" height="200"></canvas>
      <canvas id="myCanvas5" width="300" height="200"></canvas>




    </div>
    <canvas id="myCanvas6" width="300" height="200"></canvas>
    <button @click="animate()">ANIMATE</button>

    <!-- <div id="animacion">
      <div class="animacion-box"></div>
      <div class="animacion-box"></div>
      <div class="animacion-box"></div>
      <div class="animacion-box"></div>
    </div> -->
  </div>
</template>

<script>
const PI = Math.PI;

export default {
  data() {
    return {
      radius: 70,
      curr: 40,
      start: 40,
      finish: 80,
      currentStep: 0,
      segmentDegrees: 72
    }
  },
  methods: {
    handleScroll(e) {
      console.log(e.target.scrollTop);
    },

    animateCircleSegment(to = 0) {
      console.log(object)
      var canvas = document.getElementById('myCanvas3');
      var ctx = canvas.getContext('2d');
      ctx.clearRect(0, 0, 300, 200);
      ctx.beginPath();
      ctx.strokeStyle = 'orange';
      ctx.arc(150, 100, this.radius, this.start, draw_to, false);
      ctx.stroke();

      this.curr = this.curr + 1;
      console.log(this.curr);
      if (this.curr < this.finish + 1) {
        requestAnimationFrame(() => {
          // Math.PI * 2 es la circunferencia 360ª
          this.animateCircleSegment(Math.PI * 2 * this.curr / 100);
        });
      }
    },
    createAllCircles() {
      createSegment('mainCircle', gray, 0, 360, false);


    },

    createSegment(canvasName, color, from, to, clockwise) {
      const canvas = document.getElementById(canvasName);
      const context = canvas.getContext('2d');
      let centerX = canvas.width / 2;
      let centerY = canvas.height / 2;
      var radius = 70;

      context.beginPath();
      context.arc(centerX, centerY, radius, from, to , clockwise);
      context.fillStyle = 'transparent';
      context.fill();
      context.lineWidth = 5;
      context.strokeStyle = color;
      context.stroke();
    },
    getRadians(degrees) {
      return(degrees * (PI / 180));
    }

  },
  mounted() {
    //this.animateCircleSegment();

    // var canvas2 = document.getElementById('myCanvas2');
    // var context = canvas2.getContext('2d');
    // var centerX = canvas2.width / 2;
    // var centerY = canvas2.height / 2;
    // var radius = 70;

    // context.beginPath();
    // context.arc(centerX, centerY, radius, 0, 1.25664, false);
    // context.fillStyle = 'transparent';
    // context.fill();
    // context.lineWidth = 5;
    // context.strokeStyle = 'red';
    // context.stroke();

    // var canvas3 = document.getElementById('myCanvas3');
    // var context = canvas3.getContext('2d');
    // var centerX = canvas3.width / 2;
    // var centerY = canvas3.height / 2;
    // var radius = 70;

    // context.beginPath();
    // context.arc(centerX, centerY, radius, 1.25664, 2.51327, false);
    // context.fillStyle = 'transparent';
    // context.fill();
    // context.lineWidth = 5;
    // context.strokeStyle = 'blue';
    // context.stroke();

    // var canvas4 = document.getElementById('myCanvas4');
    // var context = canvas4.getContext('2d');
    // var centerX = canvas4.width / 2;
    // var centerY = canvas4.height / 2;
    // var radius = 70;

    // context.beginPath();
    // context.arc(centerX, centerY, radius, 2.51327, 5.02655, false);
    // context.fillStyle = 'transparent';
    // context.fill();
    // context.lineWidth = 5;
    // context.strokeStyle = 'orange';
    // context.stroke();

    // var canvas5 = document.getElementById('myCanvas5');
    // var context = canvas5.getContext('2d');
    // var centerX = canvas5.width / 2;
    // var centerY = canvas5.height / 2;
    // var radius = 70;

    // context.beginPath();
    // context.arc(centerX, centerY, radius, 5.02655, 2 * Math.PI, false);
    // context.fillStyle = 'transparent';
    // context.fill();
    // context.lineWidth = 5;
    // context.strokeStyle = 'green';
    // context.stroke();




    // const el = document.getElementById('animacion');
    // if(el){
    //   el.addEventListener('scroll', this.handleScroll);
    // }
  },
  destroyed() {
    //el.removeEventListener('scroll', this.handleScroll);
  }
}
</script>

<style>
  .circle-container {
    position: relative;
  }

  #myCanvas, #myCanvas2, #myCanvas3, #myCanvas4, #myCanvas5  {
    position: absolute;
    transform: rotate(-90deg);
  }

  #myCanvas6 {
    position: absolute;
    right: 0;
    transform: rotate(-90deg);
  }


</style>
