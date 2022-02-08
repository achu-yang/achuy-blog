<template>
  <div class="background-box">
    <div style="width: 100%;height: 100vh;position: relative;display: block;">
      <img id="background" alt="background" src="" width="100%" height="100%"/>
    </div>
  </div>
</template>
<script>
import {RainyDay} from "../public/js/rainyday.js"

export default{
  data(){
    return{

    }
  },
  mounted(){
    let image = document.getElementById('background');
    image.onload = function() {
        var engine = new RainyDay({
            image: this
        });
        engine.rain([ [0, 2, 200], [3, 3, 1] ], 100);
    };
    image.crossOrigin = 'anonymous';
    image.src = 'https://img0.baidu.com/it/u=1233191258,1301746421&fm=253&fmt=auto&app=138&f=JPEG?w=100%&h=275';
  }
}
</script>