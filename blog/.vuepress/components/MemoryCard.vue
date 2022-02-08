<template>
  <div class="wrap">
    <div class="box1" @click="nextQuestion">
        <div class="box">
          <div class="position-box" style="position: relative;">

            <div class="type" style="position: absolute;top: 0;left: 0;border-top-left-radius: 18px;background: #000;margin-bottom: 20px;">
              <div style="padding: 10px;">
                {{showQuestion.type}}
              </div>
            </div>

            <div class="content" style="width: 100%;;position: absolute;top: 10vh;left: 0;display: flex;" v-if="!showQuestion.question.picture">
              <div class="img-box" style="flex: 1;padding-left: 5vw;">
                <img :src="$withBase(showQuestion.question.picture)" alt="" width="400px" height="250px">
              </div>
              <div class="text-box" style="flex: 2;padding: 10px;">
                <p style="line-height: 50px;">问题描述：</p>
                <p style="text-indent:50px;line-height:50px">{{showQuestion.question.text}}</p>
              </div>
            </div>
            <div class="content" style="width: 100%;;position: absolute;top: 50px;left: 0;display: flex;padding: 10px;" v-else>
              <div class="text-box" style="flex: 2;">
                <p style="line-height: 50px;">问题描述：</p>
                <p style="text-indent:50px;line-height:50px">{{showQuestion.question.text}}</p>
              </div>
            </div>

            <div class="type" style="position: absolute;bottom: -50vh;right: 0;border-bottom-right-radius: 18px;background: #000;">
              <div style="padding: 10px;">
                <span style="color: red;">翻开</span>
              </div>
            </div>
          </div>
        </div>
        <div class="mask">
          <div class="position-box" style="position: relative;">
            <div class="type" style="position: absolute;top: 0;left: 0;border-top-left-radius: 18px;background: #000;margin-bottom: 20px;">
              <div style="padding: 10px;">
                {{showQuestion.type}}
              </div>
            </div>
            <div class="content" style="width: 100%;;position: absolute;top: 10vh;left: 0;display: flex;" v-if="showQuestion.answer.picture">
              <div class="img-box" style="flex: 1;padding-left: 5vw;">
                <img :src="$withBase(showQuestion.answer.picture)" alt="" width="400px" height="250px">
              </div>
              <div class="text-box" style="flex: 2;padding: 10px;font-size: 20px;">
                <p style="text-indent:50px;line-height:50px">{{showQuestion.answer.text}}</p>
              </div>
            </div>
            <div class="content" style="width: 100%;;position: absolute;top: 50px;left: 0;display: flex;" v-else>
              <div class="text-box" style="text-align:center;flex: 2;font-size: 20px;">
                {{showQuestion.answer.text}}
              </div>
            </div>
          </div>
        </div>
    </div>
</div>
</template>
<script>

export default{
  data(){
    return{
      questionData:null,
      showQuestion:null,
      typeInfo:{
        typeNumber:0,
      },
    }
  },
  created(){
    this.questionData = require('./question.json');
    // console.log(this.questionData)
    this.questionData['question_list'].forEach(element => {
      this.typeInfo[element['category']] = element['list'].length;
      this.typeInfo['typeNumber'] += 1;
    });
    console.log(this.typeInfo)
    this.nextQuestion();
  },
  methods:{
    nextQuestion(){
      //随机获取类别
      let randomType = this.getRandomNumberByRange(0,this.typeInfo['typeNumber']-1);
      // console.log(randomType)
      //获取该类别问题总数
      let type = this.questionData['question_list'][randomType]['category'];
      // console.log(type)
      //随机获取该类别问题
      let randomQuestion = this.getRandomNumberByRange(0,this.typeInfo[type]-1);
      // console.log(randomQuestion)
      //获取
      this.showQuestion = this.questionData['question_list'][randomType]['list'][randomQuestion];
      console.log(this.showQuestion)
      //添加
      this.showQuestion['type'] = type.toString();
    },
    getRandomNumberByRange(start, end) {
      return Math.floor(Math.random() * (end - start) + start)
    }
  }
}
</script>
<style>
.wrap {
    width: 100vw;
    margin-top: 10vh;
    height: 60vh;
    /* background-color: sandybrown; */
    position: relative;
    display: flex;
    justify-content: center;
}

.box1 {
    width: 50vw;
    height: 50vh;
    /* background-color: salmon; */
    float: left;
    /* margin: 0 5px 0 5px; */
    border-radius: 18px;
}

.box{
    width: 50vw;
    height: 50vh;
    box-sizing: border-box;
    font-size: 28px;
    border-radius: 18px;
    background-color: #fff;
    opacity: 0.5;
    /* padding: 38px 0 0 38px; */
    position: absolute;
    perspective: 1000px;
    transition: 0.5s ease-in-out;
}
.mask{
    width: 50vw;
    height: 50vh;
    background-color: #000;
    opacity: 1;
    border-radius: 18px;
    color: #fff;
    font-size: 30px;
    /* text-align: center; */
    /* line-height: 300px; */
    font-family: '微软雅黑';
    font-weight: bold;
    position: absolute;
    backface-visibility:hidden;
    perspective: 1000px;
    transform: rotateY(-180deg);
    transition: 0.5s ease-in-out;
}
.box1:hover .box{
    transform: rotateY(-180deg);
}
.box1:hover .mask{
    transform: rotateY(-360deg);
}
.box1:nth-child(1) .mask{
    color: teal;
}

</style>
