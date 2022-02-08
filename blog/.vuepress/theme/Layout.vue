<template>
  <div class="container" style="width: 100vw;height: 100vh;">
    <Background></Background>
    <div class="home-page" v-if='layoutManager.isHome' style="position: absolute;z-index: 22;left: 0;top: 0;opacity: 0.8;">
      <!-- <VHead></VHead> -->
      <MyHead></MyHead>
      <!-- <img :src="$withBase('/imgs/logo.jpg')" alt="logo"> -->
      <!-- <MyMain></MyMain> -->
      <!-- <RotateBox></RotateBox> -->
      <MemoryCard></MemoryCard>

    </div>

    <div class="classify-page" v-if='layoutManager.isClassify' style="position: absolute;z-index: 22;left: 0;top: 0;opacity: 0.7;">
      <MyHead></MyHead>
    </div>

    <div class="item-page" v-if='layoutManager.isItem' style="position: absolute;z-index: 22;left: 0;top: 0;opacity: 0.7;">
      <MyHead></MyHead>
    </div>

    <div class="other-page" v-if='layoutManager.isOther' style="position: absolute;z-index: 22;left: 0;top: 0;opacity: 0.7;">
      <MyHead></MyHead>
    </div>

    <div class="article-page" v-if='layoutManager.isArticle' style="position: absolute;z-index: 22;left: 0;top: 0;opacity: 0.7;">
      <Content />
    </div>
    
  </div>
</template>
<script>
// import VHead from './assembling_components/MyHead'
export default{
  data(){
    return{
      layoutManager:{
        currentLayout:null,
        isHome:false,
        isClassify:false,
        isItem:false,
        isOther:false,
        isAbout:false,
        isArticle:false,
      },
    }
  },
  // components:{ VHead },
  watch:{
    $route(){
      this.refreshLayout();
    },
  },
  created(){
    this.refreshLayout();
  },
  methods:{
    update(str){
      this.layoutManager[str] = true;
      this.layoutManager.currentLayout && (this.layoutManager[this.layoutManager.currentLayout] = false);
      this.layoutManager.currentLayout = str;
      this.updateView();
    },
    updateView(){
      let a = this.layoutManager;
      this.layoutManager = a;
    },
    refreshLayout(){
      let path_arg = this.$page.regularPath.split('/').splice(1)
      switch(path_arg[0]){
        case '' :
          this.update("isHome")
          break;
        case 'classify':
          this.update("isClassify")
          break;
        case 'item' :
          this.update("isItem")
          break;
        case 'other' :
          this.update("isOther")
          break;
        case 'about':
          this.update("isAbout")
          break;
        default:
          this.update("isArticle")
          break;
      }
    }
  }
}
</script>
<style>
#home{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>