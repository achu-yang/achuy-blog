<template>
  <div style="height: 300px;">
    <div class="cube-wrap">
      <div class="cube depth">
        <div class="front-pane">
          <img :src="$withBase('/imgs/front.jpg')" alt="" width="100%" height="100%">
        </div>
        <div class="back-pane">
          <img :src="$withBase('/imgs/back.jpg')" alt="" width="100%" height="100%">
        </div>
        <div class="top-pane">
          <img :src="$withBase('/imgs/top.jpg')" alt="" width="100%" height="100%">
        </div>
        <div class="bottom-pane">
          <img :src="$withBase('/imgs/bottom.jpg')" alt="" width="100%" height="100%">
        </div>
        <div class="left-pane">
          <img :src="$withBase('/imgs/left.jpg')" alt="" width="100%" height="100%">
        </div>
        <div class="right-pane">
          <img :src="$withBase('/imgs/right.jpg')" alt="" width="100%" height="100%">
        </div>
      </div>
    </div>
  </div>
</template>
<style>
/*************** ANIMATIONS ***************/
@-webkit-keyframes cube-spin {
  from { -webkit-transform: rotateY(0); }
  to { -webkit-transform: rotateY(360deg); }
}

@-ms-keyframes cube-spin {
  from { ms-transform: rotateY(0); }
  to { ms-transform: rotateY(360deg); }
}

@keyframes cube-spin {
  from { transform: rotateY(0); }
  to { transform: rotateY(360deg); }
}

@-webkit-keyframes spin-vertical {
  from { -webkit-transform: rotateX(0); }
  to { -webkit-transform: rotateX(-360deg); }
}

@-ms-keyframes spin-vertical {
  from { ms-transform: rotateX(0); }
  to { ms-transform: rotateX(-360deg); }
}

@keyframes spin-vertical {
  from { transform: rotateX(0); }
  to { transform: rotateX(-360deg); }
}

    
/*************** STANDARD CUBE ***************/
.cube-wrap {
  -webkit-perspective: 800px;
  -webkit-perspective-origin: 50% 100px;

  -moz-perspective: 800px;
  -moz-perspective-origin: 50% 100px;

  -ms-perspective: 800px;
  -ms-perspective-origin: 50% 100px;

  perspective: 800px;
  perspective-origin: 50% 100px;
}

.cube {
  position: relative;
  width: 200px;
  margin: 0 auto;
  
  -webkit-transform-style: preserve-3d;
  -webkit-animation: cube-spin 5s infinite linear;
  
  -moz-transform-style: preserve-3d;
  -moz-animation: cube-spin 5s infinite linear;

  -ms-transform-style: preserve-3d;
  -ms-animation: cube-spin 5s infinite linear;

  transform-style: preserve-3d;
  animation: cube-spin 5s infinite linear;
}

.cube div {
  position: absolute;
  width: 200px;
  height: 200px;
  background: rgba(255,255,255,0.1);
  box-shadow: inset 0 0 30px rgba(125,125,125,0.8);
  font-size: 20px;
  text-align: center;
  line-height: 200px;
  color: rgba(0,0,0,0.5);
  font-family: sans-serif;
  text-transform: uppercase;
}

.back-pane {
  -webkit-transform: translateZ(-100px) rotateY(180deg);
  -moz-transform: translateZ(-100px) rotateY(180deg);
  -ms-transform: translateZ(-100px) rotateY(180deg);

  transform: translateZ(-100px) rotateY(180deg);
}
.right-pane {
  -webkit-transform:rotateY(-270deg) translateX(100px);
  -webkit-transform-origin: top right;

  -moz-transform:rotateY(-270deg) translateX(100px);
  -moz-transform-origin: top right;

  -ms-transform:rotateY(-270deg) translateX(100px);
  -ms-transform-origin: top right;

  transform:rotateY(-270deg) translateX(100px);
  transform-origin: top right;
}
.left-pane {
  -webkit-transform:rotateY(270deg) translateX(-100px);
  -webkit-transform-origin: center left;

  -moz-transform:rotateY(270deg) translateX(-100px);
  -moz-transform-origin: center left;

  -ms-transform:rotateY(270deg) translateX(-100px);
  -ms-transform-origin: center left;

  transform:rotateY(270deg) translateX(-100px);
  transform-origin: center left;
}
.top-pane {
  -webkit-transform:rotateX(-90deg) translateY(-100px);
  -webkit-transform-origin: top center;

  -moz-transform:rotateX(-90deg) translateY(-100px);
  -moz-transform-origin: top center;

  -ms-transform:rotateX(-90deg) translateY(-100px);
  -ms-transform-origin: top center;

  transform:rotateX(-90deg) translateY(-100px);
  transform-origin: top center;
}
.bottom-pane {
  -webkit-transform:rotateX(90deg) translateY(100px);
  -webkit-transform-origin: bottom center;

  -moz-transform:rotateX(90deg) translateY(100px);
  -moz-transform-origin: bottom center;

  -ms-transform:rotateX(90deg) translateY(100px);
  -ms-transform-origin: bottom center;

  transform:rotateX(90deg) translateY(100px);
  transform-origin: bottom center;
}
.front-pane {
  -webkit-transform: translateZ(100px);
  -moz-transform: translateZ(100px);
  -ms-transform: translateZ(100px);

  transform: translateZ(100px);
}
</style>