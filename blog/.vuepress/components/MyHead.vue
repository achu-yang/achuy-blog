<template>
  <div class="head-container" style="position: relative;width: 100vw;">
    <!-- <div class="nav">
      <div class="icon-box" style="flex:5"></div>
      <div class="placeholder-box" style="flex: 65;"></div>
      <div class="nav-box" v-for='(item,index) in nav_box' :style="item.style" @mouseenter="enter(index)" @mouseleave="leave(index)">
         <RouterLink
         class="navbar-link"
         :to="item.path"
         >
          {{item.name}}
         </RouterLink> 
      </div>
    </div> -->
    <MyNav></MyNav>
    <div class="personal-review">
      <div class="kong" style="flex:1"></div>
      <div class="head-portrait" style="flex:1;position: relative;">
        <div class="head-circle" style="overflow: hidden;">
          <img :src="$withBase('/imgs/logo.jpg')" alt="" width="100%" height="100%">
        </div>
      </div>
      <div class="text-box" style="flex:1">
        <div class="blogger-name">
          Achuy
        </div>
        <div class="motto" style="color: aliceblue;">
          由经验而得的智慧，胜于学习而得的智慧！
        </div>
      </div>
      <div class="item-review-box" style="flex:2">
        <RotateBox></RotateBox>
      </div>
      <div class="kong" style="flex:1"></div>
    </div>
  </div>
</template>
<script>
export default{
  data(){
    return{
      img_url: '',
      enterColor:"red",
      leaveColor:"white",
      nav_data:[
        "Home",
        "Classify",
        "Item",
        "Other"
      ],
      nav_box:[]
    }
  },
  created(){},
  mounted(){
    this.initData();
  },
  watch:{
    $route(){
      this.initData();
    }
  },
  methods:{
    getCurrentPath(){
      let path_arg = this.$page.regularPath.split('/').splice(1)
      return '/' + path_arg[0];
    },
    initData(){
      this.nav_box = this.nav_data.map(item=>{
        return{
          name: item,
          path: this.convertPath(item),
          style:{
            flex:5,
            paddingTop: "1vh",
            color:  this.convertPath(item) === this.getCurrentPath() 
                      ? this.enterColor
                      : this.leaveColor,
            width: "5vw",
            textAlign: "center",
            fontSize: "1.3em"
          }
        }
      });
    },
    convertPath(str){
      return str === "Home" ? '/' : '/' + str.toLowerCase();
    },

    updateNavData(){
      let a = this.nav_box;
      this.nav_box = a;
    },
    enter(index){
      let item = this.nav_box[index]
      if(item.path === this.getCurrentPath())return;
      item.style.color = this.enterColor;
      this.updateNavData();
    },
    leave(index){
      let item = this.nav_box[index]
      if(item.path === this.getCurrentPath())return;
      item.style.color = this.leaveColor;
      this.updateNavData();
    },
  }
}
</script>
<style lang="stylus">
.head-container
  width 100%
  height 30vh
  /* background-color: #ddd */

.nav
  width 100%
  height 5vh 
  opacity 0.3
  background-color #ddd
  display flex

.personal-review
  width 100%
  height 25vh
  display flex
  
  .head-circle
    width 120px
    height 120px
    border-radius 50%
    background-color #fff
    /*设置元素绝对定位*/
    position absolute
    /*top 50%*/
    top 50%
    /*left 50%*/
    left 50%
    /*css3   transform 实现*/
    transform translate(-50%, -50%)
  
  .blogger-name
    /* background-color #fff */
    color #fff
    /*设置元素绝对定位*/
    position absolute
    top 40%
    font-size 2em
  
  .motto
    position absolute
    top 60%
    font-size 1em


</style>