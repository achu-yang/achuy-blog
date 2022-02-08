<template>
  <div class="container" style="height:100%;;">
    <div class="article-box" v-if="isRrfresh" style="margin-left:15%;width: 70%;">
      <div class="article-show" style="height: 60vh;">
        <MyCard
          class="article-card"
          v-for='item in showData'
          :data='item'
        ></MyCard>
      </div>
      <div style="display: flex;justify-content: center;">
        <el-pagination
          :current-page="showConfig.currentPage"
          :page-size="showConfig.pageSize"
          layout="prev, pager, next"
          :total="showConfig.total"
          @current-change="updateData"
        >
      </el-pagination>
      </div>
    </div>
    <div v-else style="display: flex;justify-content: center;">
      <i class="el-icon-loading"></i>
    </div>
  </div>
</template>
<script>
export default{
  data(){
    return{
      isRrfresh:true,
      totalData:[],
      showConfig:{
        currentPage:1,//当前页
        pageSize:3,//每页的数目
        // pagerCount:1,//展示的数目
        total:30, //数据总数
      },
      showData:[],
    }
  },
  created(){
    this.initData();
  },
  methods:{
    initData(){
      //1、获取$site.pages的元数据
      this.totalData = this.$site.pages.map(item=>{
        let re = /\/article/i ;
        let result = item.regularPath.match(re);
        item.frontmatter.date && (item.frontmatter.date 
          = item.frontmatter.date.replace("T00:00:00.000Z",""))
        if(result)return item;
      }).filter(item =>{
        //2、通过Array.filter过滤空数组
        return item
      }).filter(item =>{
        //3、过滤artcile目录定位的锚
        return !item.relativePath.match(/\article\/README.md/i);
      });
      this.showConfig.total = this.totalData.length;
      this.updateData(1)
    },
    updateData(val){
      this.isRrfresh = false;
      this.showConfig.currentPage = val;
      let begin = (this.showConfig.currentPage - 1) * this.showConfig.pageSize;
      this.showData = this.totalData.slice(begin,begin+3);
      this.simulationTimer().then(()=>{
        this.isRrfresh = true
      })
    },
    simulationTimer(){
      return new Promise(resolve=>{
        setTimeout(function(){
          resolve()
        },300)
      })
    }
  }
}
</script>