<template>
  <div class="nav">
    <div class="icon-box" style="flex:1"></div>
    <div class="placeholder-box" style="flex: 1;"></div>
    <div class="nav-box" v-for='(item,index) in nav_box' :style="item.style" @mouseenter="enter(index)" @mouseleave="leave(index)">
        <RouterLink
        class="navbar-link"
        :to="item.path"
        >
        {{item.name}}
        </RouterLink> 
    </div>
    <div class="placeholder-box" style="flex: 2;"></div>
  </div>
</template>
<script>
  export default{
    data(){
      return{
        enterColor:"#FFFFFF",
        leaveColor:"#0000FF",
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
              flex:1,
              paddingTop: "3vh",
              color:  this.convertPath(item) === this.getCurrentPath() 
                        ? this.enterColor
                        : this.leaveColor,
              width: "5vw",
              textAlign: "center",
              fontSize: "1.3em",
              backgroundColor:"#000",
              margin:"1vh 3vw",
              borderRadius:"10px"
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
    height 10vh 
    opacity 0.3
    /* background-color #ddd */
    display flex
  
  
  </style>