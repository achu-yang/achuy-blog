<template>
  <div class="card-container">
    <RouterLink
    class="navbar-link"
    :to="data.path"
    >
      <div class="mouse-box" :style="boxStyle">
        <div class="one-row" style="display:flex;">
          <div class="time-box"
            style="flex:1"
          >
            <div style="width: 60px;height: 60px;margin: 10px;background-color: #aef;">
              <div class="date-box" style="text-align:center;font-size: 1.5em;color: #fff;">
                {{data.frontmatter.date.split("-")[0]}}
              </div>
              <div class="date-box" style="
                text-align:center;font-size: 1.2em;color: #fff;"
              >
                {{data.frontmatter.date.split("-")[1]}} - {{data.frontmatter.date.split("-")[2]}}
              </div>
            </div>
          </div>
          <div class="title-box"
            style="flex:5;font-size: 2.5em;font-weight:500;margin-top: 1vh;"
          >
          {{data.title}}
          </div>
        </div>
        <div class="two-row">{{data.frontmatter.describe}}</div>
        <div class="three-row"></div>
      </div>
    </RouterLink> 
    
  </div>
</template>
<script>
export default{
  data(){
    return{
      boxStyle:{
        height:" 16vh",
        margin:" 2vh 0",
        backgroundColor: "#fff",
        borderRadius: "10px"
      }
    }
  },
  created(){
    console.log(this.data)
  },
  props:["data"],
  methods:{
    // enter(){
    //   this.boxStyle.height = "10vh"
    //   this.boxStyle.boxShadow = "0 0 20px 50px #ddd";
    //   this.update();
    // },
    // leave(){
    //   delete this.boxStyle.boxShadow;
    //   this.update()
    // },
    // update(){
    //   let a = this.boxStyle;
    //   this.boxStyle = a;
    //   console.log(this.boxStyle)
    // }
  }
}
</script>
<style lang="stylus">
.mouse-box
  box-shadow 0 0 0 0 

.mouse-box:hover
  box-shadow 3px 3px 10px #ddd
</style>