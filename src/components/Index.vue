<template>
  <div class="hello">
    <div class="date" id="date">{{ date }}</div>
    <div class="time" id="time">{{ time }}</div>
    <div classs="bottom">
      <div class="item"><a target="_blank" :href="url_github"><img :src="img_url_github" style="height:25px;margin-bottom:11px;" alt></a></div>
      <div class="item"><a target="_blank" :href="url_bili"><img :src="img_url_bili" style="height:35px;margin-bottom:10px;" alt></a></div>
      <div class="item">
        <el-switch
          v-model="switchValue"
          active-color="gray"
          active-value="1"
          inactive-value="2"
          @change="changeColor()"
          style="margin-bottom:35px;">
        </el-switch>
      </div>
      <div class="item"><a target="_blank" :href="url_zhihu"><img :src="img_url_zhihu" alt></a></div>
      <div class="item"><a target="_blank" :href="url_juejin"><img :src="img_url_juejin" style="height:38px;margin-bottom:6px;" alt></a></div>
    </div>
    <div><el-button id="fullornot" type="text" @click="hideAndShow()">■■■■</el-button></div>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data () {
    return {
      date: '',
      time: '',
      switchValue: '1',
      url_zhihu: 'https://www.zhihu.com/people/huang-da-fa-29-93',
      url_bili: 'https://space.bilibili.com/349834035',
      url_github: 'https://github.com/bhuangdev',
      url_juejin: 'https://juejin.cn/user/3483695904464199',
      img_url_zhihu: require('@/assets/zhihu.svg'),
      img_url_bili: require('@/assets/bili.svg'),
      img_url_github: require('@/assets/github.svg'),
      img_url_juejin: require('@/assets/juejin.svg'),
      fullState: false
    }
  },
  mounted(){
    var that = this;
    setInterval(
      function(){ 
        that.showTime(); 
      }, 1000
    );
  },
  methods:{
    showTime(){
      var myDate = new Date(); //实例一个时间对象；
      var year = myDate.getFullYear();   //获取系统的年；
      var month = myDate.getMonth()+1;   //获取系统月份，由于月份是从0开始计算，所以要加1
      var day = myDate.getDate(); // 获取系统日，
      var hour = myDate.getHours(); //获取系统时，
      var minute = myDate.getMinutes(); //分
      var second = myDate.getSeconds(); //秒
      
      this.date = month + '月' + day + '日';
      this.time = this.addZero(hour) + ':' + this.addZero(minute) + ':' + this.addZero(second);
    },
    addZero(data){
      if(Number(data) < 10){
        data = '0' + data;
      }
      return data;
    },
    changeColor(){
      if(this.switchValue == '2'){
        document.getElementById("fullornot").style.color = "rgb(255, 255, 255)";
        document.getElementById("date").style.color = "rgb(0,0,0)";
        document.getElementById("time").style.color = "rgb(0,0,0)";
        document.body.style.backgroundColor = "rgb(255, 255, 255)";
        this.img_url_github = require('@/assets/github2.svg')
      }else{
        document.getElementById("fullornot").style.color = "rgb(0,0,0)";
        document.getElementById("date").style.color = "rgb(255, 255, 255)";
        document.getElementById("time").style.color = "rgb(255, 255, 255)";
        document.body.style.backgroundColor = "rgb(0,0,0)";
        this.img_url_github = require('@/assets/github.svg')
      }
    },
    hideAndShow(){
      if(this.fullState){
        this.fullState = false;
        this.cancelFullScreen();
      }else {
        this.fullState = true;
        this.fullScreen();
      }
    },
    fullScreen()  
    {  
      var docElm = document.documentElement;  
      //W3C   
      if (docElm.requestFullscreen) {  
          docElm.requestFullscreen();  
      }  
          //FireFox   
      else if (docElm.mozRequestFullScreen) {  
          docElm.mozRequestFullScreen();  
      }  
          //Chrome等   
      else if (docElm.webkitRequestFullScreen) {  
          docElm.webkitRequestFullScreen();  
      }  
          //IE11   
      else if (elem.msRequestFullscreen) {  
          elem.msRequestFullscreen();  
      }  
    },
    cancelFullScreen() {  
      if (document.exitFullscreen) {  
          document.exitFullscreen();  
      }  
      else if (document.mozCancelFullScreen) {  
          document.mozCancelFullScreen();  
      }  
      else if (document.webkitCancelFullScreen) {  
          document.webkitCancelFullScreen();  
      }  
      else if (document.msExitFullscreen) {  
          document.msExitFullscreen();  
      }  
    }
  }
}
</script>

<style scoped>
.hello{
  left:50px;
  right:50px;
  margin-top:53%;
}
#date{
  font-size:200px;
  color:#fff;
  font-weight: bold;
}
#time{
  font-size:260px;
  color:#fff;
  font-weight: bold;
}
.bottom{
  text-align: center;
}
.item{
  display: inline-block;
  margin-left:40px;
  margin-top:20px;
}
#fullornot{
  text-align:center;
  color:black
}
</style>
