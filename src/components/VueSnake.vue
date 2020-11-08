<template>
  <div class="hello">
    
    <canvas id="snake" width="400" height="400"></canvas>
    
  </div>
</template>

<script>
const FPS = 15;

export default {
  name: 'VueSnake',
  props: {
    backgroundColor: {
      type: String,
      default: '#efefef'
    },
    snakeColor: {
      type: String,
      default: '#42b983'
    },
    appleColor: {
      type: String,
      default: '#ddd'
    },
    gameSpeed: {
      type: Number,
      default: 5
    }
  },
  data: () => {
    return {
      px: 10,
      py: 10,
      gs: 20,
      tc: 20,
      ax: 15,
      ay: 15,
      xv: 0,
      yv: 0,
      trail: [],
      tail: 5,
      canv: null,
      ctx: null,
    }
  },
  methods: {
    setupCanvas() {
      this.canv = document.getElementById("snake");
      this.ctx = this.canv.getContext("2d");
    },
    setupGame() {
      document.addEventListener("keydown", this.keyPush);
      setInterval(this.nextFrame, 1000 / FPS);
    },
    nextFrame() {
      this.px+=this.xv;
      this.py+=this.yv;
      if(this.px<0) {
          this.px= this.tc-1;
      }
      if(this.px>this.tc-1) {
          this.px= 0;
      }
      if(this.py<0) {
          this.py= this.tc-1;
      }
      if(this.py>this.tc-1) {
          this.py= 0;
      }
      this.ctx.fillStyle=this.backgroundColor;
      this.ctx.fillRect(0,0,this.canv.width,this.canv.height);
  
      this.ctx.fillStyle=this.snakeColor;
      for(var i=0;i<this.trail.length;i++) {
          this.ctx.fillRect(this.trail[i].x*this.gs,this.trail[i].y*this.gs,this.gs-2,this.gs-2);
          if(this.trail[i].x==this.px && this.trail[i].y==this.py) {
              this.tail = 5;
          }
      }
      this.trail.push({x:this.px,y:this.py});
      while(this.trail.length>this.tail) {
        this.trail.shift();
      }
  
      if(this.ax==this.px && this.ay==this.py) {
          this.tail++;
          this.ax=Math.floor(Math.random()*this.tc);
          this.ay=Math.floor(Math.random()*this.tc);
      }
      this.ctx.fillStyle=this.appleColor;
      this.ctx.fillRect(this.ax*this.gs,this.ay*this.gs,this.gs-2,this.gs-2);
    },
    keyPush(evt) {
      console.log(evt)
      switch(evt.keyCode) {
        case 37:
          this.xv=-1;this.yv=0;
          break;
        case 38:
          this.xv=0;this.yv=-1;
          break;
        case 39:
          this.xv=1;this.yv=0;
          break;
        case 40:
          this.xv=0;this.yv=1;
          break;
      }
    }
  },
  mounted() {
    this.setupCanvas()
    this.setupGame()
  },
}
</script>

<style scoped>
</style>
