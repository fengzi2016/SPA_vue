<template>
  <v-layout column>
    <v-flex xs12 class="text-xs-center" mt-5>
      <h3>Home page</h3>
    </v-flex>
    <v-flex class="text-xs-center" mt-5>
      <p>This is a user's home page</p>
    </v-flex>
    <div class="carousel">
      <transition-group tag="ul" class="slide-ul" name="list">
        <li v-for="(image,index) in urls" :key="index" v-show="index===currentIndex" @mouseenter='stop' @mouseleave='go' name='item'>
          <a :href="image.link"></a>
          <img :src="image.url" :alt='image.url'>
        </li>
      </transition-group>
      <div class="carouselNum">
        <span v-for="(num,index) in urls.length" :class="{'active':index===currentIndex}" :key="index"  @mousemove="changeIndex(index)"></span>
      </div>
    </div>
  </v-layout>
</template>

<script>
export default {
 data(){
   return{
     urls:[
       {url:'http://echarts.baidu.com/echarts2/doc/asset/img/slide-01.png',link:'#'},
        {url:'http://echarts.baidu.com/echarts2/doc/asset/img/slide-02.png',link:'#'},
         {url:'http://echarts.baidu.com/echarts2/doc/asset/img/slide-03.png',link:'#'},
          {url:'http://echarts.baidu.com/echarts2/doc/asset/img/slide-04.png',link:'#'},
           {url:'http://echarts.baidu.com/echarts2/doc/asset/img/slide-05.jpg',link:'#'}
     ],
     currentIndex:0,
     timeOut:''
   }   
 },
 methods:{
   created:function(){
   this.$nextTick(()=>{
     this.timeOut=setInterval(()=>{
       this.autoPlay()
     },4000)
   })
 },
 go:function() 
  {
   this.timeOut=setInterval(()=>{
     this.autoPlay()
   },4000)
 },
 stop:function(){
   clearInterval(this.timeOut);
   this.timeOut=null;
 },
 changeIndex:function(index){
   this.currentIndex=index;
 },
 autoPlay:function(){
   this.currentIndex++;
   if(this.currentIndex>this.urls.length-1){
     this.currentIndex=0;
   }
 }

 }
 
}
</script>
<style>
.carousel{
  position: relative;
  min-width: 1280px;
  height: 400px;
  overflow: hidden;
  background-color: #fff;
}
.slide-ul{
  width: 100%;
  height: 100%;
  
}
.slide-ul li{
    position:absolute;
    width: 100%;
    height: 100%;
  }
.carouselNum{
  position: absolute;
  z-index: 3;
  top: 380px;
  width: 100%;
  margin: 0,auto;
  text-align: center;
  font-size: 0;
}
span{
  display: inline-block;
  height: 6px;
  width: 30px;
  margin: 0 3px;
  background-color: #b2b2b2;
  cursor: pointer;
}
.active{
  background-color: white;
}
</style>

