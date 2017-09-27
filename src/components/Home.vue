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
        <li v-for="(image,index) in urls" :key="index"  @mouseenter='stop' @mouseleave='go' name='item'  :class="{'currentLi':index===currentIndex,'lastLi':index===currentIndex-1}" >
          <a :href="image.link"></a>
          <img :src="image.url" :alt='image.url'>
        </li> 
      </transition-group>

       <!-- <transition-group tag="ul" class="new-ul" name="list2" class={"Animating":anti}>
        <li v-for="(image,index) in urls" :key="index"   @mouseenter='stop' @mouseleave='go' name='item'>
          <a :href="image.link"></a>
          <img :src="image.url" :alt='image.url'>
        </li>
      </transition-group>
      <div class="carouselNum">
        <span v-for="(num,index) in urls.length" :class="{'active':index===currentIndex}" :key="index"  @mousemove="changeIndex(index)"></span>
      </div>
    </div> -->
    <!-- <div class="css-carousel">
      <transition-group tag="ul"  name="css-list" class="css-slide-ul" :class="{'stopAnima':ifStop}" >
        <li v-for="(item,index) in urls" :key="index" @mouseenter='stopAnima' @mouseleave='goAnima' name='item-css'>
        <a :href="item.link" :key="index" >
        <img :src="item.url" :alt='item.url' :key="index">
        </a>
      </li>
      </transition-group>
      <div class="css-carouselNum">
        <span v-for="(num,index) in urls.length" :class="{'active':index===currentIndex}" :key="index"  @mousemove="changeIndex(index)"></span>
      </div>   -->
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
     timeOut:'',
     ifStop:false,
     ani:false,
   
   }   
 },
 methods:{
   created:function(){
   this.$nextTick(()=>{
     this.timeOut=setInterval(()=>{
       this.autoPlay();
      //  this.ani=!this.ani;
     },2000)
   });
 },
 go:function() 
  {
   this.timeOut=setInterval(()=>{
     this.autoPlay();
    // this.ani=!this.ani;
   },6000);
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
 },
    stopAnima:function(){
      this.ifStop=true;
    },
    goAnima:function(){
      this.ifStop=false;
    }

 }
 
}
</script>
<style>
.new-ul{
  list-style:none; /* 将默认的列表符号去掉 */
  padding:0; /* 将默认的内边距去掉 */
  margin:0; /* 将默认的外边距去掉 */
  width:8000px;
  height: 100%;
  position: absolute;
}
.new-ul li{
    display: inline;
  }
.Animating{
 transform: translateX(-1280px);
}
@keyframes new-ul {
  0%{
    left: 0;
  }
  100%{
    left: -1280px;
  }
}

.carousel{
  position: relative;
  min-width: 1280px;
  height: 400px;
  overflow: hidden;
  background-color: #fff;
}
.slide-ul{
  list-style:none; /* 将默认的列表符号去掉 */
  padding:0; /* 将默认的内边距去掉 */
  margin:0; /* 将默认的外边距去掉 */
  width:8000px;
  height: 100%;
  position: relative;
  
  /* animation:change 40s linear 2s infinite; */
}
.slide-ul li{
    /* display:none; */
    /* display: inline; */
    position:absolute;
    left:0px;
  }
.currentLi{
  z-index: 9;
  animation: current 4s linear 2s;
}
.lastLi{
  z-index: 10;
  animation:last 4s linear 2s;
}
@keyframes current {
  0%{
    left:1280px;
  }
  100%{
    left: 0;
  }
}
@keyframes last {
  0%{
    left:0px;
  }
  100%{
    left:-1280px;
  }
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
/* .currentLi{
 position: relative;
 animation: out 2s linear 2s;
}
.nextLi{
  position: relative;
  animation: in 2s linear 2s;
} */
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
/* @keyframes out{
  0%{
  left: 0px ;
  }

  100%{
    left:-1280px;
  }
}
@keyframes in {
  0%{
    right:0px ;
  }
  100%{
    left:-1280px;
  }
} */


 @keyframes change{
  0%{
    left: 0px;
  }
  10%{
    left: 0px;
  }
  20%{
    left: -1280px;
  }
  30%{
    left: -1280px;
  }
  40%{
    left: -2560px;
  }
  50%{
     left: -2560px;
  }
  60%{
    left: -3840px;
  }
  70%{
    left: -3840px;
  }
  80%{
    left:-5120px;
  }
  90%{
     left:-5120px;
  }
  100%{
    left: 0px;
  }
}

.css-carousel{
  position: relative;
  min-width: 1280px;
  height: 400px;
  /* overflow: hidden; */
  background-color: #fff;
}
.css-slide-ul{
 list-style:none;  
  padding:0; 
  margin:0;
  width:8000px;
  height: 100%;
  position: relative;
  /* animation:change 40s linear 2s infinite; */
}
/* .slide-out{
  position: relative;
  animation:change 4s linear 4s infinite;
} */
.stopAnima{
  animation-play-state: paused;
}
/* .slide-into{
  list-style:none;  
  padding:0; 
  margin:0; 
  width: 100%;
  height: 100%;
  position: relative;
  animation:into 4s linear 4s infinite;
} */
.css-slide-ul li{
  list-style:none;  
  padding:0; 
  margin:0; 
  display: inline;
  /* animation:change 4s linear 4s;
  position: relative; */
}
</style>

